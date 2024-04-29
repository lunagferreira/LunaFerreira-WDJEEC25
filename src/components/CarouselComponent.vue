<template>
  <Carousel>
    <Slide v-for="(content, index) in slideContents" :key="index">
      <div class="carousel__item">{{ content }}</div>
    </Slide>
    <template #addons>
      <Navigation />
    </template>
  </Carousel>
</template>

<script>
import { defineComponent } from 'vue';
import { Carousel, Slide } from 'vue3-carousel';
import 'vue3-carousel/dist/carousel.css';

export default defineComponent({
  name: 'CarouselComponent',
  components: {
    Carousel,
    Slide
  },
  data() {
    return {
      slideContents: [
        '1', // Content for the 1st slide
        '2', 
        '3', 
        '4'  
      ]
    };
  },
})
</script>

<style scoped>
.carousel__item {
  height: 90vh; /* 90% of the viewport height */
  width: 98%;
  background-color: #376099;
  color: white; /* Text color */
  font-size: 40px;
  border-radius: 20px; /* Rounded corners */
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
