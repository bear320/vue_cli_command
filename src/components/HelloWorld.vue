<template>
    <div class="hello" :class="type">
        <!-- <div class="img">
            <img src="../assets/logo.png" alt="Vue logo" />
            <img :src="require('@/assets/logo.png')" alt="Vue logo" />
        </div> -->
        <div class="img" v-for="item in 3" :key="item">
            <img
                :src="require(`@/assets/images/fileType/fileType${item}.png`)"
                alt=""
            />
        </div>
        <!-- <div
            class="img"
            :style="{ backgroundImage: `url(${require('@/assets/logo.png')})` }"
        ></div> -->
        <div class="text">
            <p>{{ title }}</p>
            <p>{{ msg }}</p>
            <button>Click me!</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "HelloWorld",
    props: {
        title: String,
        msg: String,
        type: String,
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.hello {
    width: 100%;
    display: inline-flex;
    margin: 1rem;
}
.wide {
    width: 50%;
}
.img {
    width: 8rem;
    height: 8rem;
    background-color: #ddd;
    img {
        width: 100%;
        height: 100%;
        vertical-align: top;
    }
}
.text {
    margin: 0 1rem;
    text-align: left;
}
</style>
