<template>
    <div class="news">
        <Images
            link="https://images.unsplash.com/photo-1504711434969-e33886168f5c?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80"
        />
        <h1>This is a news page</h1>
        <HelloWorld title="News Test" />
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
