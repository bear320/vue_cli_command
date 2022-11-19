<template>
    <div class="home">
        <img alt="Vue logo" src="../assets/logo.png" />
        <HelloWorld title="Title 1" msg="Lorem ipsum dolor sit amet." />
        <HelloWorld title="Title 2" msg="Lorem ipsum dolor sit amet." />
        <HelloWorld title="Title 3" msg="Lorem ipsum dolor sit amet." />
    </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
    name: "HomeView",
    components: {
        HelloWorld,
    },
};
</script>
