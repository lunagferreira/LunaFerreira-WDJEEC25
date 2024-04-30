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
            <h3 class="workshop-workshop">Workshop</h3>
            <h3 class="workshop-by">by Vestas</h3>
            <p>{{ content.description }}</p>
          </div>
          <div v-else-if="index === 3" class="image-slide">
            <img :src="content.src" :alt="content.alt" class="responsive-image" />
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
          title: 'Integration of Wind Farms into Electricity Grids', 
          subtitle: 'Workshop by Vestas',  
          description: 'This workshop will cover the representation of wind farms in simulation software, with an emphasis on wind turbine design and electrical performance for compliance with grid requirements.'
        },
        { 
          type: 'image',
          src: require('@/assets/challenge.png'),
          alt: 'Description'
        }
        ]
    };
    },
})
</script>

<style scoped>
.carousel__item {
  height: 80vh; /* 80% of the viewport height */
  width: 95%;
  background-color: #008ADF;
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
  padding: 1rem 3rem; /* 1rem top and bottom, 2rem left and right */
  border-radius: 32px;
  background: #E0DFDF; 
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  font-family: 'Arial', sans-serif;
  width: 42%;
  box-sizing: border-box;
}

.workshop-slide h2, .workshop-slide h3, .workshop-slide p {
  text-align: left; 
  width: 100%;
}

.workshop-slide h2 {
  font-weight: bold;
  font-size: 2rem;
  margin-bottom: 0.5rem;
  color: #898A8D;
}

.workshop-slide .workshop-workshop, .workshop-slide .workshop-by {
  font-weight: bold;
  font-size: 1.5rem;
  color: #898A8D;
  margin: 0;
}

.workshop-slide .workshop-by {
  margin-top: 0.5rem; 
}

.workshop-slide p {
  font-size: 1.3rem;
  color: #898A8D;
  line-height: 1.5;
  margin-top: 2rem;
}

.image-slide img.responsive-image {
  max-width: 60%;
  height: auto; 
}
</style>

