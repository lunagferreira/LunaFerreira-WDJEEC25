<template>
  <div>
    <Carousel v-model="slideIndex">
      <Slide v-for="(content, index) in slideContents" :key="index">
        <div class="carousel__item">
          <div v-if="typeof content === 'object' && content.question">
            {{ content.question }}
          </div>
          <div v-else>
            {{ content }}
          </div>
        </div>
      </Slide>
      <template #addons>
        <Navigation />
      </template>
    </Carousel>
    <!-- Answer outside the carousel -->
    <div class="slide-answer" v-if="slideContents[slideIndex].answer">
      Answer: {{ slideContents[slideIndex].answer }}
    </div>
  </div>
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
        slideIndex: 0,
        slideContents: [
        { question: "What is the capital of Portugal?", answer: "Lisbon" },
        'Enter a date:', 
        'Slide 3', 
        'Slide 4'
        ]
    };
    },
})
</script>

<style scoped>
.carousel__item {
  height: 80vh; /* 80% of the viewport height */
  width: 95%;
  background-color: #376099;
  color: white; /* Text color */
  font-size: 40px;
  border-radius: 20px; /* Rounded corners */
  display: flex;
  justify-content: center;
  align-items: center;
}
  
.slide-answer {
  margin-top: 20px;
  font-size: 32px;
  color: #c1701a; 
  text-align: center;
}
</style>

