<template>
    <div class="wrapper">
        <main>
            <header>
                Search: <input type="text" v-model="search" />
                <br />
                Price between US$
                <input id="min" type="number" v-model="min" /> and US$
                <input id="max" type="number" v-model="max" />
            </header>
            <template v-if="load">Loading</template>
            <template v-else>
                <div class="productContainer">
                    <div
                        class="product-item"
                        v-for="(item, index) in product"
                        :key="item.id"
                    >
                        <h3>{{ item.title }}</h3>
                        <p>{{ parseRating(item.rating) }}</p>
                        <img :src="item.image" :alt="item.title" />
                        <p>{{ parsePrice(item.price) }}</p>
                        <div>
                            <button @click="reduceCount(index, item)">-</button>
                            <input
                                type="number"
                                min="0"
                                v-model.number="count[index]"
                            />
                            <button @click="addCount(index, item)">+</button>
                        </div>
                    </div>
                </div>
            </template>
        </main>
        <aside>
            Order
            <ul>
                <li v-for="(item, index) in order" :key="item.id">
                    {{ index }}-{{ item.title }}: {{ item.count }}
                </li>
            </ul>
            <h2>Total: {{ total }}</h2>
        </aside>
    </div>
</template>

<script>
export default {
    data() {
        return {
            search: "",
            min: 0,
            max: 0,
            load: false,
            source: [],
            sourceCount: 0,
            order: [],
            count: [],
        };
    },
    computed: {
        product() {
            let cache = this.source;
            // ??????????????????
            if (this.min > 0) {
                cache = cache.filter((item) => {
                    return item.price > this.min;
                });
            }
            // ??????????????????
            if (this.max > 0) {
                cache = cache.filter((item) => {
                    return item.price < this.max;
                });
            }
            // ??????????????????
            if (this.search !== "") {
                cache = cache.filter((item) => {
                    return item.title.includes(this.search);
                });
            }
            return cache;
        },
        total() {
            if (this.product.length > 0) {
                let total = 0;
                for (const countIndex in this.product) {
                    total +=
                        this.count[countIndex] *
                        this.product[countIndex]["price"];
                }
                return parseInt(total);
            } else {
                return 0;
            }
        },
    },
    watch: {
        total: {
            handler: function (newVal, oldVal) {
                if (newVal > 10000) {
                    alert("You're gonna be broke until payday.");
                }
            },
            // ????????????????????? false??? --> ????????????????????????????????????
            // deep: true,
        },
    },
    methods: {
        parseRating(rating) {
            if (!rating) return null;
            let starStr = "";
            const star = parseInt(rating.rate);
            for (let index = 0; index < star; index++) {
                starStr += "??????";
            }
            return `${starStr} (${rating.count})`;
        },
        parsePrice(price) {
            return `US$${parseInt(price)}`;
        },
        getResource() {
            this.load = true;
            fetch("https://fakestoreapi.com/products")
                .then((res) => res.json())
                .then((json) => {
                    this.source = json;
                    // ?????????????????????
                    for (let item in this.product) {
                        this.count.push(0);
                    }
                    this.load = false;
                    this.sourceCount = this.source.length;
                    // console.log(`mothods: ${this.sourceCount}`);
                });
        },
        addCount(index, item) {
            this.count[index] += 1;
            // ????????????????????? (orderItem) ????????????????????? (item)
            // const exist = this.order.some((orderItem) => orderItem.id === item.id);
            // -------
            // ?????????????????????????????????????????????????????? id ????????? count
            // ????????????????????????
            const productIndex = this.order.findIndex(
                (orderItem) => orderItem.id === item.id
            );
            if (productIndex >= 0) {
                // ????????????????????? + 1
                this.order[productIndex]["count"] += 1;
            } else {
                // productIndex ???????????? -1
                // ????????????????????????????????????????????????????????????????????????
                this.order.push({
                    id: item.id,
                    title: item.title,
                    price: item.price,
                    count: 1, // init
                });
            }
        },
        reduceCount(index, item) {
            if (this.count[index] <= 0) return;
            this.count[index] -= 1;
            const productIndex = this.order.findIndex(
                (orderItem) => orderItem.id === item.id
            );
            if (productIndex < 0) return;
            if (this.order[productIndex]["count"] > 1) {
                this.order[productIndex]["count"] -= 1;
            } else {
                this.order.splice(productIndex, 1);
            }
        },
        getStorage() {
            let data = localStorage.getItem("testShop");
            data = JSON.parse(data);
            this.order = data ? data : [];
        },
        setStorage() {
            // ????????????????????????
            const data = JSON.stringify(this.order);
            localStorage.setItem("testShop", data);
        },
    },
    created() {
        //   console.log("created");
    },
    mounted() {
        this.getResource();
        //   console.log("mounted");
    },
    beforeUnmount() {
        //   alert("beforeUnmount");
        //   console.log("beforeUnmount");
    },
};
</script>

<style>
.wrapper {
    width: 100%;
    height: 80vh;
}
main {
    display: inline-block;
    width: calc(100vw - 21rem);
    overflow: scroll;
}
aside {
    display: inline-block;
    width: 20rem;
    vertical-align: top;
}
.productContainer {
    display: inline-flex;
}
.product-item {
    width: 200px;
    margin: 10px;
}
img {
    height: 5rem;
}
</style>
