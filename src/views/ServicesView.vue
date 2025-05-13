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
    title: 'Disaster Response',
    description:
      'Providing immediate relief and long-term rehabilitation for communities affected by natural disasters.',
    image: '/src/components/icons/palestine.svg',
  },
]

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
    <div class="first-section">
      <section class="hero">
        <div class="intro-text-wrapper">
          <div class="introTe">
            <h1 style="color: black">Our <span style="color: #9f1a1c">Services</span></h1>
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
        <img src="/src/components/icons/palestine.svg" alt="services illustration" />
      </section>
    </div>

    <div class="second-section">
      <div class="projects-wrapper">
        <div class="introTe">
          <h1 style="color: black">Featured <span style="color: #9f1a1c">Projects</span></h1>
        </div>

        <p>
          Explore our ongoing and completed projects that make a difference in people's lives and
          contribute to nation-building.
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
}

.first-section {
  width: 100%;
  display: flex;
  flex-direction: row;
  background: #ffffff;
  align-items: center;
  justify-content: center;
}

.second-section {
  width: 100%;
  padding: 4rem;
  display: flex;
  flex-direction: row;
  background: #ffffff;
  align-items: center;
  justify-content: center;
}

.projects-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  width: 100%;
}

.intro-text-wrapper {
  display: flex;
  justify-content: center;
  flex-direction: column;
  margin-top: 1rem;
  padding-left: 15rem;
}

.donate-wrapper {
  display: flex;
  justify-content: left;
  margin-top: 1rem;
}

.hero {
  padding: 4rem 2rem;
  width: 50%;
  background: #ffffff;
}

.content {
  max-width: 1200px;
  width: 50%;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.content img {
  width: 91.5%;
  height: auto;
}

.introTe {
  display: flex;
  flex-direction: row;
  justify-content: left;
  align-items: center;
  gap: 0.5rem;
}

.introTe h1 {
  font-size: 62px;
}

p {
  margin-bottom: 2rem;
  width: 75%;
}

.donate-btn {
  background: #dc1b28;
  color: white;
  padding: 0.5rem 1.5rem;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.donate-btn:hover {
  background: #b01520;
}

/* Carousel Styles */
.carousel {
  position: relative;
  width: 80%;
  max-width: 900px;
  margin: 2rem auto;
  overflow: hidden;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
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
  padding-bottom: 2rem;
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
  font-size: 1.5rem;
  color: #fff;
}

.carousel-caption p {
  margin: 0 auto;
  width: 90%;
  font-size: 1rem;
  line-height: 1.4;
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

@media (max-width: 1024px) {
  .first-section {
    flex-direction: column;
  }

  .hero {
    width: 100%;
    padding: 2rem 1rem;
  }

  .content {
    width: 100%;
    justify-content: center;
  }

  .intro-text-wrapper {
    padding-left: 0;
    align-items: center;
    text-align: center;
  }

  .introTe {
    justify-content: center;
  }

  .introTe h1 {
    font-size: 48px;
  }

  .donate-wrapper {
    justify-content: center;
  }

  .carousel {
    width: 90%;
  }

  .carousel-item img {
    height: 300px;
  }
}

@media (max-width: 768px) {
  .introTe h1 {
    font-size: 36px;
  }

  .carousel-item img {
    height: 250px;
  }

  .carousel-caption h3 {
    font-size: 1.2rem;
  }

  .carousel-caption p {
    font-size: 0.9rem;
  }

  .carousel-control {
    width: 40px;
    height: 40px;
    font-size: 1.2rem;
  }
}

@media (max-width: 480px) {
  .introTe h1 {
    font-size: 28px;
  }

  .carousel-item img {
    height: 200px;
  }

  .carousel-caption {
    padding: 1rem;
  }

  .carousel-caption h3 {
    font-size: 1rem;
  }

  .carousel-caption p {
    font-size: 0.8rem;
  }

  .carousel-control {
    width: 35px;
    height: 35px;
    font-size: 1rem;
  }

  .carousel-indicators span {
    width: 8px;
    height: 8px;
  }
}
</style>
