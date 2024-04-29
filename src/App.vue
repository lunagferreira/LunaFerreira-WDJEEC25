<template>
  <div>
    <Carousel v-model="slideIndex">
      <Slide v-for="(content, index) in slideContents" :key="index">
        <div class="carousel__item">
          <div v-if="typeof content === 'object' && content.question">
            {{ content.question }}
          </div>
          <!-- Check for date input type -->
          <div v-else-if="typeof content === 'object' && content.type === 'date'">
            <div>{{ content.prompt }}</div>
            <input type="date" v-model="dateInput" class="date-input">
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
    <!-- Display the date -->
    <div v-if="dateInput && slideIndex === 1" class="date-display">
      Selected date: {{ dateInput }}
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
        dateInput: '',
        slideContents: [
        { question: "What is the capital of Portugal?", answer: "Lisbon" },
        { prompt: "Enter a date:", type: "date" },
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

.date-input {
  margin-top: 10px;
  padding: 8px;
  width: 70%;
  font-size: 32px; 
}

.slide-answer {
  margin-top: 20px;
  font-size: 32px;
  color: #e84396; 
  text-align: center;
}

.date-display {
  margin-top: 20px;
  font-size: 32px;
  color: #e84396; 
  text-align: center;
}
</style>

