<template>
    <div class="news">
        <Images link="https://fakeimg.pl/100/" />
        <Images link="https://fakeimg.pl/150/" />
        <h1>This is a news page</h1>
        <HelloWorld title="News Test" type="wide" />
    </div>
</template>

<script>
import HelloWorld from "@/components/HelloWorld.vue";
import Images from "@/components/Images.vue";

export default {
    name: "NewsView",
    components: {
        HelloWorld,
        Images,
    },
};
</script>
