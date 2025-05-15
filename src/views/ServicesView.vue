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
    image: '/src/components/icons/s1.png',
  },
  {
    title: 'Community Development',
    description:
      'Empowering communities through livelihood programs, infrastructure development, and capacity building.',
    image: '/src/components/icons/s2.png',
  },
  {
    title: 'Environmental Sustainability',
    description:
      'Implementing projects that promote environmental conservation, renewable energy, and sustainable practices.',
    image: '/src/components/icons/s3.png',
  },
  {
    title: 'Disaster Response',
    description:
      'Providing immediate relief and long-term rehabilitation for communities affected by natural disasters.',
    image: '/src/components/icons/s4.png',
  },
]

const parameters = [
  {
    number: '01',
    title: 'Addresses a community need',
    points: [
      'Has the capacity to increase income levels and generate employment',
      'Uplift the living conditions of the beneficiaries.',
    ],
  },
  {
    number: '02',
    title: 'Aligns with our core business',
    points: [
      'Relates to the core businesses of our strategic business units (SBUs) – power, banking and financial services, food, infrastructure, and land.',
    ],
  },
  {
    number: '03',
    title: 'Helps our business or creates competitive advantage for the Business Units (BUs)',
    points: [
      'Helps increase revenues and lower costs',
      'Enhances key stakeholder relationships with local government unit, host community, etc.',
    ],
  },
  {
    number: '04',
    title: "Aligns with the Aboitiz Foundation's programs",
    points: [
      "Aligns with the foundation's program of education, enterprise development, environment, including disaster risk reduction and resilience",
    ],
  },
  {
    number: '05',
    title: 'Sustainable and scalable',
    points: [
      'Has potential for growth and expansion',
      'Creates lasting impact beyond initial implementation',
    ],
  },
  {
    number: '06',
    title: 'Measurable impact',
    points: ['Has clear metrics for success', 'Allows for transparent reporting of outcomes'],
  },
  {
    number: '07',
    title: 'Collaborative approach',
    points: [
      'Involves multiple stakeholders in planning and execution',
      'Leverages partnerships for greater impact',
    ],
  },
]

const activeParameter = ref(0)

const nextParameter = () => {
  activeParameter.value = (activeParameter.value + 1) % parameters.length
}

const prevParameter = () => {
  activeParameter.value = (activeParameter.value - 1 + parameters.length) % parameters.length
}

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
    <div class="hero-banner">
      <img src="/src/components/icons/IP2.jpg" alt="Services banner" class="banner-image" />
      <div class="banner-overlay"></div>
    </div>

    <div class="content-box">
      <div class="decorative-line left"></div>
      <div class="decorative-circle top-right"></div>
      <div class="decorative-circle bottom-left"></div>
      <div class="content-text">
        <div class="introTe">
          <h1>Our <span class="accent">Services</span></h1>
        </div>
        <p>
          The Aboitiz Foundation delivers impactful programs and services across various sectors,
          creating sustainable change in communities through our partnerships and initiatives.
        </p>
      </div>
      <div class="decorative-line right"></div>
    </div>

    <div class="second-section">
      <div class="projects-wrapper">
        <div class="projects-content">
          <div class="introTe">
            <h1>Featured <span class="accent">Projects</span></h1>
          </div>

          <p class="projects-description">
            Explore our ongoing and completed projects that make a difference in people's lives and
            contribute to nation-building.
          </p>

          <div class="button-wrapper">
            <a href="/contact" class="volunteer-btn">Volunteer</a>
          </div>
        </div>

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

    <div class="parameters-section">
      <div class="parameters-header">
        <h2>Seven Parameters</h2>
        <p>
          To ensure that our projects deliver the much needed results for our communities, we
          encourage development of carefully-designed interventions that are inclusive,
          collaborative, and scalable. From the traditional charitable projects or dole-outs, we
          have been transforming the way we do CSR and following the CSR 2.0 parameters towards
          inclusive impact.
        </p>
      </div>

      <div class="parameters-grid desktop-only">
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

      <div class="parameters-carousel mobile-only">
        <button class="param-nav prev" @click="prevParameter">❮</button>
        <div class="param-slide">
          <div class="parameter-number">{{ parameters[activeParameter].number }}</div>
          <div class="parameter-content">
            <h3>{{ parameters[activeParameter].title }}</h3>
            <ul>
              <li
                v-for="(point, pointIndex) in parameters[activeParameter].points"
                :key="pointIndex"
              >
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
  font-size: 18px;
}

.hero-banner {
  width: 100%;
  height: 400px;
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

.content-box {
  width: 100%;
  background: #9f1a1c;
  color: white;
  padding: 2rem 0;
  margin-top: -5rem;
  position: relative;
  overflow: hidden;
  z-index: 10;
  text-align: center;
}

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
  justify-content: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.introTe h1 {
  font-size: 3.5rem;
  font-weight: bold;
  color: white;
  position: relative;
}

.accent {
  color: #ffffff;
  font-weight: bold;
  text-shadow: 3px 3px 6px rgba(0, 0, 0, 0.3);
}

.content-box p {
  color: #ffffff;
  line-height: 1.7;
  margin-bottom: 0;
  font-size: 1.2rem;
}

.second-section {
  width: 100%;
  padding: 5rem 1rem;
  background: #ffffff;
}

.projects-wrapper {
  display: flex;
  flex-direction: row;
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
  justify-content: flex-start;
}

.projects-content .introTe h1 {
  color: black;
  font-size: 3rem;
  text-align: left;
}

.projects-content .accent {
  color: #9f1a1c;
  font-weight: bold;
  text-shadow: none;
}

.projects-description {
  margin: 1.5rem 0;
  color: #000000;
  font-size: 1.2rem;
  line-height: 1.7;
  max-width: 100%;
}

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
  font-size: 1.1rem;
}

.volunteer-btn:hover {
  background: white;
  color: #9f1a1c;
  transform: translateY(-2px);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
  border: 1px solid #9f1a1c;
}

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

.carousel-item:hover .carousel-caption,
.carousel-control:hover + .carousel-inner .carousel-caption,
.carousel-control:hover ~ .carousel-inner .carousel-caption,
.carousel-control:hover ~ .carousel-item .carousel-caption {
  opacity: 1;
  pointer-events: auto;
}

.carousel-caption h3 {
  margin: 0 0 0.5rem 0;
  font-size: 1.8rem;
  color: #fff;
}

.carousel-caption p {
  margin: 0 auto;
  width: 90%;
  font-size: 1.1rem;
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

.parameters-section {
  width: 100%;
  padding: 5rem 1rem;
  background: #e2e2e2;
  position: relative;
  overflow: hidden;
}

.parameters-section::before {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  width: 300px;
  height: 300px;
  background: rgba(159, 26, 28, 0.05);
  border-radius: 50%;
  transform: translate(30%, -30%);
}

.parameters-header {
  max-width: 900px;
  margin: 0 auto 4rem auto;
  text-align: center;
}

.parameters-header h2 {
  font-size: 3rem;
  font-weight: bold;
  color: #333;
  margin-bottom: 1.5rem;
  position: relative;
  display: inline-block;
}

.parameters-header h2::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 3px;
  background: #9f1a1c;
  border-radius: 2px;
}

.parameters-header p {
  color: #000000;
  line-height: 1.7;
  max-width: 800px;
  margin: 0 auto;
  font-size: 1.2rem;
}

.parameters-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: auto auto;
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.parameters-grid .parameter-card:nth-child(n + 4) {
  grid-column: span 1;
}

.parameters-grid .parameter-card:nth-child(7) {
  grid-column: 2 / span 1;
}

.parameter-card {
  background: white;
  border-radius: 8px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08);
  overflow: hidden;
  transition: all 0.3s ease;
  display: flex;
  flex-direction: column;
  height: 100%;
  position: relative;
  border-top: 4px solid #9f1a1c;
}

.parameter-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.12);
}

.parameter-number {
  font-size: 3rem;
  font-weight: 800;
  color: #9f1a1c;
  padding: 1.5rem 1.5rem 0 1.5rem;
  line-height: 1;
}

.parameter-content {
  padding: 0 1.5rem 1.5rem 1.5rem;
  flex-grow: 1;
  display: flex;
  flex-direction: column;
}

.parameter-content h3 {
  font-size: 1.4rem;
  font-weight: 600;
  color: #333;
  margin-bottom: 1rem;
  line-height: 1.3;
}

.parameter-content ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.parameter-content li {
  position: relative;
  padding-left: 1.5rem;
  margin-bottom: 0.75rem;
  color: #000000;
  line-height: 1.5;
  text-align: left;
  font-size: 1.1rem;
}

.parameter-content li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0.5rem;
  width: 8px;
  height: 8px;
  background: #9f1a1c;
  border-radius: 50%;
}

.parameters-carousel {
  max-width: 500px;
  margin: 0 auto;
  position: relative;
  padding: 0 2rem;
}

.param-slide {
  background: white;
  border-radius: 8px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08);
  padding: 2rem;
  border-top: 4px solid #9f1a1c;
  min-height: 300px;
}

.param-nav {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(159, 26, 28, 0.8);
  color: white;
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  z-index: 5;
  font-size: 1.2rem;
  transition: all 0.3s ease;
}

.param-nav.prev {
  left: 0;
}

.param-nav.next {
  right: 0;
}

.param-nav:hover {
  background: #9f1a1c;
}

.param-indicators {
  display: flex;
  justify-content: center;
  margin-top: 1.5rem;
}

.param-indicators span {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: rgba(159, 26, 28, 0.3);
  margin: 0 5px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.param-indicators span.active {
  background: #9f1a1c;
  transform: scale(1.2);
}

.desktop-only {
  display: grid;
}

.mobile-only {
  display: none;
}

@media (max-width: 1200px) {
  .projects-wrapper {
    gap: 2rem;
  }

  .decorative-line.left {
    left: 2%;
  }

  .decorative-line.right {
    right: 2%;
  }

  .hero-banner {
    height: 600px;
  }
}

@media (max-width: 992px) {
  .projects-wrapper {
    flex-direction: column;
  }

  .projects-content {
    text-align: center;
    padding-top: 0;
  }

  .projects-content .introTe {
    justify-content: center;
  }

  .projects-content .introTe h1 {
    text-align: center;
  }

  .button-wrapper {
    justify-content: center;
  }

  .carousel {
    margin-top: 2rem;
    width: 100%;
  }

  .parameters-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .parameters-grid .parameter-card:nth-child(7) {
    grid-column: 1 / span 2;
  }

  .introTe h1 {
    font-size: 3rem;
  }

  .parameters-header h2 {
    font-size: 2.5rem;
  }

  .decorative-line {
    display: none;
  }

  .hero-banner {
    height: 500px;
  }
}

@media (max-width: 768px) {
  .hero-banner {
    height: 400px;
  }

  .content-box {
    margin-top: -3rem;
    padding: 1.5rem 0;
  }

  .introTe h1 {
    font-size: 2.5rem;
  }

  .content-box p {
    font-size: 1.1rem;
  }

  .carousel-item img {
    height: 300px;
  }

  .parameters-header h2 {
    font-size: 2.2rem;
  }

  .parameters-header p {
    font-size: 1.1rem;
  }

  .desktop-only {
    display: none;
  }

  .mobile-only {
    display: block;
  }

  .projects-content .introTe h1 {
    font-size: 2.5rem;
  }

  .projects-description {
    font-size: 1.1rem;
  }

  .decorative-circle {
    opacity: 0.5;
  }
}

@media (max-width: 480px) {
  .hero-banner {
    height: 300px;
  }

  .introTe h1 {
    font-size: 2rem;
  }

  .content-box p {
    font-size: 1rem;
  }

  .volunteer-btn {
    padding: 0.6rem 1.8rem;
    font-size: 1rem;
  }

  .parameters-header h2 {
    font-size: 1.8rem;
  }

  .parameters-header p {
    font-size: 1rem;
  }

  .projects-content .introTe h1 {
    font-size: 2rem;
  }

  .projects-description {
    font-size: 1rem;
  }

  .carousel-caption h3 {
    font-size: 1.5rem;
  }

  .carousel-caption p {
    font-size: 1rem;
  }
}
</style>
