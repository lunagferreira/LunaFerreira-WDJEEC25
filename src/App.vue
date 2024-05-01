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
/* Styles specific to each carousel item */
.carousel__item {
  height: 80vh; /* 80% of the viewport height */
  width: 90%;
  /* background-color: #008ADF; */
  background-image: linear-gradient(to right, #009BDF, #0056B3); /* Blue gradient from lighter to darker */
  color: white; /* Text color */
  font-size: 40px;
  border-radius: 20px; /* Rounded corners */
  display: flex;
  justify-content: center; /* Horizontally */
  align-items: center; /* Vertically */
  padding: 20px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1), 
              0 0 10px 4px #58cbf1; /* Neon effect */
  transition: box-shadow 0.3s ease-in-out;
}

/* Styles for the date input inside the carousel */
.date-input {
  margin-top: 10px;
  padding: 8px;
  width: 70%;
  font-size: 32px; 
}

/* Styles for displaying answers and date selections outside the carousel */
.slide-answer, .date-display {
  margin-top: 20px;
  font-size: 32px;
  color: #e84396; 
  text-align: center;
}

/* Specific styles for the workshop information slide */
.workshop-slide {
  flex-direction: column; /* Stack children vertically */
  align-items: flex-start; /* Align children to the start of the cross axis */
  justify-content: center; /* Center children along the main axis */
  padding: 1rem 3rem; /* 1rem top and bottom, 2rem left and right */
  border-radius: 32px;
  background: #E0DFDF; 
  font-family: 'Arial', sans-serif;
  width: 42%;
  box-sizing: border-box;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3); 
}

/* General styling for titles and paragraphs */
.workshop-slide h2, .workshop-slide h3, .workshop-slide p {
  text-align: left; 
  width: 100%;
}

/* Title styles */
.workshop-slide h2 {
  font-weight: bold;
  font-size: 2rem;
  margin-bottom: 0.5rem;
  color: #898A8D;
}

/* Subtitle styles */
.workshop-slide .workshop-workshop, .workshop-slide .workshop-by {
  font-weight: bold;
  font-size: 1.5rem;
  color: #898A8D;
  margin: 0;
}

.workshop-slide .workshop-by {
  margin-top: 0.5rem; /* Space above 'by Vestas' */
}

/* Description Styles */
.workshop-slide p {
  font-size: 1.3rem;
  color: #898A8D;
  line-height: 1.5;
  margin-top: 2rem;
}

/* Navigation and other interaction elements */
.Navigation, .image-slide img {
  cursor: pointer;
  transition: transform 0.3s ease; /* Smooth transition for hover effects */
}

.Navigation:hover, .image-slide img:hover {
  transform: scale(1.05); /* Slight scale to indicate interactivity */
}

/* Image Styles */
.image-slide img.responsive-image {
  max-width: 50%;
  height: auto; 
}
</style>

