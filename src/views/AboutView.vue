<template>
    <div class="about">
        <h1>This is an about page</h1>
        <Button type="primary">Primary</Button>
        <hr />
        <div>
            <Carousel v-model="value" loop>
                <CarouselItem v-for="item in 3" :key="item">
                    <!-- <div class="demo-carousel">{{ item }}</div> -->
                    <div>
                        <img
                            :src="
                                require(`@/assets/images/fileType/fileType${item}.png`)
                            "
                        />
                    </div>
                </CarouselItem>
                <!-- <CarouselItem>
                    <div class="demo-carousel">2</div>
                </CarouselItem>
                <CarouselItem>
                    <div class="demo-carousel">3</div>
                </CarouselItem>
                <CarouselItem>
                    <div class="demo-carousel">4</div>
                </CarouselItem> -->
            </Carousel>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            value: 0,
        };
    },
};
</script>
