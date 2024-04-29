<template>
  <Carousel>
    <Slide v-for="slide in 4" :key="slide">
      <div class="carousel__item">JEEC</div>
    </Slide>
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
})
</script>

<style scoped>
.carousel__item {
  height: 90vh; /* 90% of the viewport height */
  width: 90%;
  background-color: #955fa1;
  color: white; /* Text color */
  font-size: 40px;
  border-radius: 20px; /* Rounded corners */
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
