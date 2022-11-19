<template>
    <div class="hello">
        <div class="img">
            <img src="" alt="" />
        </div>
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
.img {
    width: 8rem;
    height: 8rem;
    background-color: #ddd;
}
.text {
    margin: 0 1rem;
    text-align: left;
}
</style>
