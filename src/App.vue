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
          <div v-else-if="index === 2" class="workshop-slide">
            <h2>{{ content.title }}</h2>
            <h3>{{ content.subtitle }}</h3>
            <p>{{ content.description }}</p>
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
        {
          type: 'workshop', 
          title: 'Integration of Wind Farms into Electricity Grids Workshop', 
          subtitle: 'by Vestas', 
          description: 'This workshop will cover the representation of wind farms in simulation software, with an emphasis on wind turbine design and electrical performance for compliance with grid requirements.'
        },
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

.workshop-slide {
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
  padding: 2rem;
  border-radius: 16px;
  background: #dbdbdb; 
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  font-family: 'Arial', sans-serif;
  width: 50%;
  box-sizing: border-box;
}

.workshop-slide h2 {
  font-weight: bold;
  font-size: 2rem;
  margin-bottom: 0.5rem;
  color: #8c8c8c;
}

.workshop-slide h3 {
  font-weight: normal;
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
  color: #8c8c8c;
}

.workshop-slide p {
  font-size: 1rem;
  color: #8c8c8c;
  line-height: 1.5;
}
</style>

