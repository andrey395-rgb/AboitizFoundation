<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const currentSlide = ref(0)
const isTransitioning = ref(false)
let intervalId: number | undefined
const isHovered = ref(false)

const projects = [
  {
    title: 'Education Initiatives',
    description:
      'Providing access to quality education through school building projects, scholarship programs, and teacher training.',
    image: '/src/components/icons/palestine.svg',
  },
  {
    title: 'Community Development',
    description:
      'Empowering communities through livelihood programs, infrastructure development, and capacity building.',
    image: '/src/components/icons/palestine.svg',
  },
  {
    title: 'Environmental Sustainability',
    description:
      'Implementing projects that promote environmental conservation, renewable energy, and sustainable practices.',
    image: '/src/components/icons/palestine.svg',
  },
  {
    title: "Disaster Response",
    description: "Providing immediate relief and long-term rehabilitation for communities affected by natural disasters.",
    image: "/src/components/icons/palestine.svg"
  }
];

const nextSlide = () => {
  if (isTransitioning.value) return
  isTransitioning.value = true
  currentSlide.value = (currentSlide.value + 1) % projects.length
  setTimeout(() => (isTransitioning.value = false), 500)
}

const prevSlide = () => {
  if (isTransitioning.value) return
  isTransitioning.value = true
  currentSlide.value = (currentSlide.value - 1 + projects.length) % projects.length
  setTimeout(() => (isTransitioning.value = false), 500)
}

const goToSlide = (index: number) => {
  if (isTransitioning.value || currentSlide.value === index) return
  isTransitioning.value = true
  currentSlide.value = index
  setTimeout(() => (isTransitioning.value = false), 500)
}

const startAutoScroll = () => {
  intervalId = window.setInterval(() => {
    if (!isHovered.value) nextSlide()
  }, 3000)
}

const stopAutoScroll = () => {
  if (intervalId) {
    clearInterval(intervalId)
  }
}

onMounted(() => {
  startAutoScroll()
})

onUnmounted(() => {
  stopAutoScroll()
})
</script>

<template>
  <div class="services">
    <!-- Hero Banner - Doubled height -->
    <div class="hero-banner">
      <img
        src="/src/components/icons/palestine.svg"
        alt="Services banner"
        class="banner-image"
      />
      <div class="banner-overlay"></div>
    </div>

          <p>
            The Aboitiz Foundation delivers impactful programs and services across various sectors,
            creating sustainable change in communities through our partnerships and initiatives.
          </p>
          <div class="donate-wrapper">
            <a href="#" class="donate-btn">Donate</a>
          </div>
        </div>
      </section>

      <section class="content">
        <img
          src="/src/components/icons/palestine.svg"
          alt="services illustration"
        />
      </section>
    </div>

    <!-- Featured Projects Section - Side by side layout -->
    <div class="second-section">
      <div class="projects-wrapper">
        <div class="projects-content">
          <div class="introTe">
            <h1>Featured <span class="accent">Projects</span></h1>
          </div>

        <p>
          Explore our ongoing and completed projects that make a difference in people's lives
          and contribute to nation-building.
        </p>

        <div class="carousel" @mouseenter="isHovered = true" @mouseleave="isHovered = false">
          <div class="carousel-inner" :style="{ transform: `translateX(-${currentSlide * 100}%)` }">
            <div class="carousel-item" v-for="(project, index) in projects" :key="index">
              <img :src="project.image" :alt="project.title" />
              <div class="carousel-caption hover-target">
                <h3>{{ project.title }}</h3>
                <p>{{ project.description }}</p>
              </div>
            </div>
          </div>

          <button class="carousel-control prev hover-target" @click="prevSlide">❮</button>
          <button class="carousel-control next hover-target" @click="nextSlide">❯</button>

          <div class="carousel-indicators">
            <span
              v-for="(project, index) in projects"
              :key="index"
              :class="{ active: currentSlide === index }"
              @click="goToSlide(index)"
            ></span>
          </div>
        </div>
      </div>
    </div>

    <!-- Seven Parameters Section with Creative Design -->
    <div class="parameters-section">
      <div class="parameters-header">
        <h2>Seven Parameters</h2>
        <p>
          To ensure that our projects deliver the much needed results for our communities, we encourage development of carefully-designed interventions that are inclusive, collaborative, and scalable. From the traditional charitable projects or dole-outs, we have been transforming the way we do CSR and following the CSR 2.0 parameters towards inclusive impact.
        </p>
      </div>

      <!-- Desktop view - Adjusted grid layout: 3 in first row, 4 in second row -->
      <div class="parameters-grid desktop-only">
        <!-- First row: parameters 1-3 -->
        <div v-for="(param, index) in parameters.slice(0, 3)" :key="index" class="parameter-card">
          <div class="parameter-number">{{ param.number }}</div>
          <div class="parameter-content">
            <h3>{{ param.title }}</h3>
            <ul>
              <li v-for="(point, pointIndex) in param.points" :key="pointIndex">
                {{ point }}
              </li>
            </ul>
          </div>
        </div>

        <!-- Second row: parameters 4-7 -->
        <div v-for="(param, index) in parameters.slice(3)" :key="index + 3" class="parameter-card">
          <div class="parameter-number">{{ param.number }}</div>
          <div class="parameter-content">
            <h3>{{ param.title }}</h3>
            <ul>
              <li v-for="(point, pointIndex) in param.points" :key="pointIndex">
                {{ point }}
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Mobile view - Carousel style -->
      <div class="parameters-carousel mobile-only">
        <button class="param-nav prev" @click="prevParameter">❮</button>
        <div class="param-slide">
          <div class="parameter-number">{{ parameters[activeParameter].number }}</div>
          <div class="parameter-content">
            <h3>{{ parameters[activeParameter].title }}</h3>
            <ul>
              <li v-for="(point, pointIndex) in parameters[activeParameter].points" :key="pointIndex">
                {{ point }}
              </li>
            </ul>
          </div>
        </div>
        <button class="param-nav next" @click="nextParameter">❯</button>

        <div class="param-indicators">
          <span
            v-for="(_, index) in parameters"
            :key="index"
            :class="{ active: activeParameter === index }"
            @click="activeParameter = index"
          ></span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.services {
  width: 100%;
  display: flex;
  flex-direction: column;
  background: #ffffff;
  align-items: center;
  justify-content: center;
  font-size: 18px; /* Increased base font size */
}

/* Hero Banner Styles - Doubled height */
.hero-banner {
  width: 100%;
  height: 400px; /* Doubled from 400px to 800px */
  position: relative;
  overflow: hidden;
}

.banner-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.banner-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.4);
}

/* Content Box Styles - Thinner height */
.content-box {
  width: 100%;
  background: #9f1a1c; /* Red background */
  color: white; /* White text */
  padding: 2rem 0; /* Reduced padding to make it thinner */
  margin-top: -5rem;
  position: relative;
  overflow: hidden;
  z-index: 10;
  text-align: center; /* Center text */
}

/* Decorative elements */
.decorative-line {
  position: absolute;
  height: 3px;
  background: rgba(255, 255, 255, 0.2);
  width: 150px;
}

.decorative-line.left {
  top: 50%;
  left: 5%;
  transform: translateY(-50%);
}

.decorative-line.right {
  top: 50%;
  right: 5%;
  transform: translateY(-50%);
}

.decorative-circle {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
}

.decorative-circle.top-right {
  width: 200px;
  height: 200px;
  top: -100px;
  right: 10%;
}

.decorative-circle.bottom-left {
  width: 150px;
  height: 150px;
  bottom: -75px;
  left: 15%;
}

.content-text {
  position: relative;
  z-index: 2;
  max-width: 800px;
  margin: 0 auto;
  padding: 0 2rem;
}

.introTe {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center; /* Center title */
  gap: 0.5rem;
  margin-bottom: 1rem; /* Reduced margin to make it more compact */
}

.introTe h1 {
  font-size: 3.5rem; /* Increased font size */
  font-weight: bold;
  color: white;
  position: relative;
}

.accent {
  color: #ffffff;
  font-weight: bold;
  text-shadow: 3px 3px 6px rgba(0, 0, 0, 0.3); /* Added shadow effect */
}

.content-box p {
  color: #ffffff;
  line-height: 1.7;
  margin-bottom: 0;
  font-size: 1.2rem; /* Increased font size */
}

/* Featured Projects Section - Side by side layout */
.second-section {
  width: 100%;
  padding: 5rem 1rem;
  background: #ffffff;
}

.projects-wrapper {
  display: flex;
  flex-direction: row; /* Changed to row for side-by-side layout */
  align-items: flex-start;
  max-width: 1200px;
  margin: 0 auto;
  gap: 3rem;
}

.projects-content {
  flex: 1;
  text-align: left;
  padding-top: 2rem;
}

.projects-content .introTe {
  justify-content: flex-start; /* Left align title */
}

.projects-content .introTe h1 {
  color: black;
  font-size: 3rem; /* Increased font size */
  text-align: left;
}

.projects-content .accent {
  color: #9f1a1c;
  font-weight: bold;
  text-shadow: none;
}

.projects-description {
  margin: 1.5rem 0;
  color: #000000; /* Changed to black for better readability */
  font-size: 1.2rem; /* Increased font size */
  line-height: 1.7;
  max-width: 100%;

}

/* Volunteer button moved under Featured Projects */
.button-wrapper {
  display: flex;
  margin-top: 2rem;
}

.volunteer-btn {
  background: #9f1a1c;
  color: white;
  padding: 0.75rem 2.5rem;
  border-radius: 4px;
  transition: all 0.3s ease;
  font-weight: 600;
  text-decoration: none;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  font-size: 1.1rem; /* Increased font size */
}

.volunteer-btn:hover {
  background: white;
  color: #9f1a1c;
  transform: translateY(-2px);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
  border: 1px solid #9f1a1c;
}

/* Carousel Styles */
.carousel {
  flex: 1.5;
  position: relative;
  overflow: hidden;
  border-radius: 8px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.15);
}

.carousel-inner {
  display: flex;
  transition: transform 0.5s ease;
}

.carousel-item {
  min-width: 100%;
  position: relative;
  flex-shrink: 0;
}

.carousel-item img {
  width: 100%;
  height: 400px;
  object-fit: cover;
  display: block;
}

.carousel-caption {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 1.5rem;
  text-align: center;
  opacity: 0;
  transition: opacity 0.3s ease;
  padding-bottom: 2.4rem;
  pointer-events: none;
}

/* Show overlay when hovering over image or carousel arrows */
.carousel-item:hover .carousel-caption,
.carousel-control:hover + .carousel-inner .carousel-caption,
.carousel-control:hover ~ .carousel-inner .carousel-caption,
.carousel-control:hover ~ .carousel-item .carousel-caption {
  opacity: 1;
  pointer-events: auto;
}

.carousel-caption h3 {
  margin: 0 0 0.5rem 0;
  font-size: 1.8rem; /* Increased font size */
  color: #fff;
}

.carousel-caption p {
  margin: 0 auto;
  width: 90%;
  font-size: 1.1rem; /* Increased font size */
  line-height: 1.5;
  color: #ffffff;
}

.carousel-control {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  padding: 1rem;
  cursor: pointer;
  font-size: 1.5rem;
  z-index: 10;
  border-radius: 50%;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
}

.carousel-control.prev {
  left: 20px;
}

.carousel-control.next {
  right: 20px;
}

.carousel-control:hover {
  background: rgba(0, 0, 0, 0.8);
  transform: translateY(-50%) scale(1.1);
}

.carousel-indicators {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
  position: absolute;
  bottom: 20px;
  left: 0;
  right: 0;
}

.carousel-indicators span {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.5);
  margin: 0 5px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.carousel-indicators span.active {
  background: #9f1a1c;
  transform: scale(1.2);
}

.carousel-indicators span:hover {
  background: rgba(255, 255, 255, 0.8);
}
</style>
