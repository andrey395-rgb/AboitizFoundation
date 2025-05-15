<script setup lang="ts">
import { ref, onMounted } from 'vue';
import Donate from '../components/Donate.vue'; // Import the Donate component

// Add state for controlling the donate modal
const isDonateModalOpen = ref(false);

// Function to open the donate modal
const openDonateModal = () => {
  isDonateModalOpen.value = true;
};

// Function to close the donate modal
const closeDonateModal = () => {
  isDonateModalOpen.value = false;
};

// Handle donation submission
const handleDonationSubmit = (formData: any) => {
  console.log('Donation submitted:', formData);
  // Process the donation - you would typically send this to your backend
  // Show a success message or redirect to a thank you page
  closeDonateModal();
};

const coreValues = [
  {
    title: 'INTEGRITY',
    description:
      'We believe in integrity. We deliver on what we promise, practice fair processes, are accountable for our actions and their consequences.',
    icon: '/src/components/icons/honest.png',
  },
  {
    title: 'TEAMWORK',
    description:
      'We believe in teamwork. We apply a multi-disciplinary approach to achieve our business goals. We work independently while promoting cooperation and mutual respect.',
    icon: '/src/components/icons/collaborate.png',
  },
  {
    title: 'INNOVATION',
    description:
      'We believe in innovation. We constantly look for better ways to provide efficient systems, quality service and products.',
    icon: '/src/components/icons/innovation.png',
  },
  {
    title: 'RESPONSIBILITY',
    description:
      'We believe in responsibility. We adhere to good corporate governance, advocate organizational and environmental sustainability, and care for all our stakeholders.',
    icon: '/src/components/icons/social-responsibility.png',
  },
]

const activeValueIndex = ref(0)
const isTransitioning = ref(false)
const touchStartX = ref(0)
const touchEndX = ref(0)

const handleTouchStart = (e) => {
  touchStartX.value = e.touches[0].clientX
}

const handleTouchMove = (e) => {
  touchEndX.value = e.touches[0].clientX
}

const handleTouchEnd = () => {
  if (isTransitioning.value) return

  const swipeThreshold = 50
  const diff = touchStartX.value - touchEndX.value

  if (Math.abs(diff) > swipeThreshold) {
    isTransitioning.value = true
    if (diff > 0) {
      activeValueIndex.value = (activeValueIndex.value + 1) % coreValues.length
    } else {
      activeValueIndex.value = (activeValueIndex.value - 1 + coreValues.length) % coreValues.length
    }
    setTimeout(() => (isTransitioning.value = false), 500)
  }
}

const partners = [
  { name: 'Aboitiz Power', logo: '/src/components/icons/partner1.png' },
  { name: 'Aboitiz Equity Ventures', logo: '/src/components/icons/partner2.png' },
  { name: 'Union Bank', logo: '/src/components/icons/partner3.png' },
  { name: 'Pilmico', logo: '/src/components/icons/partner4.png' },
  { name: 'Aboitiz InfraCapital', logo: '/src/components/icons/partner5.png' },
  { name: 'Aboitiz Land', logo: '/src/components/icons/partner6.png' },
  { name: 'Republic Cement', logo: '/src/components/icons/partner7.png' },
  { name: 'Aboitiz Foundation', logo: '/src/components/icons/partner8.png' },
]

const observeElements = () => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible')
        }
      })
    },
    { threshold: 0.1 },
  )

  document.querySelectorAll('.fade-in').forEach((el) => {
    observer.observe(el)
  })
}

onMounted(() => {
  observeElements()
})
</script>

<template>
  <div class="home">
    <div class="first-home">
      <section class="hero">
        <div class="intro-text-wrapper fade-in">
          <div class="introTe">
            <h1>Who <span class="accent">We Are</span></h1>
          </div>

          <p>
            The Aboitiz Group's commitment to giving back traces its roots over a century ago. This
            legacy has been instilled and passed on through generations of its corporate history,
            with the help of our partners.
          </p>
          <div class="button-wrapper">
            <a href="#" class="donate-btn" @click.prevent="openDonateModal">Donate</a>
          </div>
        </div>
      </section>

      <section class="content fade-in">
        <div class="image-container">
          <img
            src="/src/components/icons/IP1.jpg"
            alt="Children benefiting from Aboitiz Foundation programs"
          />
          <!-- <div class="decorative-circle top-right"></div> -->
          <!-- <div class="decorative-circle bottom-left"></div> -->
        </div>
      </section>
    </div>

    <div class="banner-section">
      <div class="banner-image">
        <img src="/src/components/icons/groupaboitiz.png" alt="Aboitiz Foundation Impact" />
        <div class="banner-overlay"></div>
      </div>
    </div>

    <div class="second-home">
      <div class="partners-container fade-in">
        <div class="decorative-line left"></div>
        <!-- <div class="decorative-circle top-right"></div> -->
        <!-- <div class="decorative-circle bottom-left"></div> -->

        <div class="partners-content">
          <div class="introTe">
            <h1>Our <span class="accent">Partners</span></h1>
          </div>

          <p>
            We partner with the Aboitiz business units. Together with the Aboitiz Business Units, we
            develop and implement CSR projects that aim to co-create safe, empowered, and
            sustainable communities. Tagged as CSR 2.0, our projects deliver long-term benefits, are
            aligned with our core competencies, encourage team member engagement, and are scalable
            initiatives with positive sustainable impact of national scope.
          </p>

          <div class="partners-logo-grid">
            <a
              v-for="(partner, index) in partners"
              :key="index"
              href="https://www.aboitizconstructioninc.com/"
              target="_blank"
              rel="noopener noreferrer"
              class="partner-logo-link"
            >
              <img :src="partner.logo" :alt="partner.name + ' logo'" class="partner-logo" />
            </a>
          </div>
        </div>
      </div>
    </div>

    <div class="map-container fade-in">
      <div class="map-header">
        <h1>Our <span class="accent">Reach</span></h1>
        <p class="map-description">
          Discover the locations where Aboitiz Foundation is making a positive impact across the
          Philippines.
        </p>
      </div>

      <div class="map-section">
        <iframe
          class="map-embed"
          src="https://www.google.com/maps/d/u/0/embed?mid=1NBYf_O7PJTmSs1sjaknUWhbYFhgZC0w&ehbc=2E312F"
          title="Aboitiz Foundation Impact Locations"
        ></iframe>
      </div>
    </div>

    <div class="core-values-section fade-in">
      <div class="core-values-header">
        <h1>The Aboitiz Way: <span class="accent">Our Core Values</span></h1>
        <p>
          For over a hundred years of doing business, we in the Aboitiz Group have nurtured and
          strengthened our core values and beliefs that guide us to be the best at what we do, and
          embolden us to uphold our mission of creating long-term value for all our stakeholders.
        </p>
      </div>

      <div class="value-cards-container desktop-only">
        <div v-for="(value, index) in coreValues" :key="index" class="value-card">
          <div class="first-part">
            <img :src="value.icon" :alt="value.title + ' icon'" />
            <h2>{{ value.title }}</h2>
          </div>
          <p>{{ value.description }}</p>
        </div>
      </div>

      <div
        class="values-carousel mobile-only"
        @touchstart="handleTouchStart"
        @touchmove="handleTouchMove"
        @touchend="handleTouchEnd"
      >
        <div class="value-slide">
          <div class="first-part">
            <img
              :src="coreValues[activeValueIndex].icon"
              :alt="coreValues[activeValueIndex].title + ' icon'"
            />
            <h2>{{ coreValues[activeValueIndex].title }}</h2>
          </div>
          <p>{{ coreValues[activeValueIndex].description }}</p>
        </div>

        <div class="value-indicators">
          <span
            v-for="(_, index) in coreValues"
            :key="index"
            :class="{ active: activeValueIndex === index }"
            @click="activeValueIndex = index"
          ></span>
        </div>
      </div>
    </div>

    <!-- Donate Modal Component -->
    <Donate
      :isOpen="isDonateModalOpen"
      @close="closeDonateModal"
      @submit="handleDonationSubmit"
    />
  </div>
</template>

<style scoped>
/* Your existing styles remain unchanged */
.home {
  width: 100%;
  display: flex;
  flex-direction: column;
  background: #ffffff;
  font-size: 18px;
}

h1 {
  font-size: 3.5rem;
  font-weight: bold;
  line-height: 1.2;
}

p {
  font-size: 1.2rem;
  line-height: 1.7;
  color: #333;
}

.accent {
  color: #9f1a1c;
  font-weight: bold;
}

.fade-in {
  opacity: 0;
  transform: translateY(20px);
  transition:
    opacity 0.8s ease,
    transform 0.8s ease;
}

.fade-in.visible {
  opacity: 1;
  transform: translateY(0);
}

.first-home {
  width: 100%;
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 5rem 2rem;
  max-width: 1440px;
  margin: 0 auto;
}

.hero {
  width: 50%;
  padding-right: 2rem;
}

.intro-text-wrapper {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.introTe {
  display: flex;
  align-items: center;
  margin-bottom: 1.5rem;
}

.button-wrapper {
  margin-top: 1rem;
}

.donate-btn {
  background: #9f1a1c;
  color: white;
  font-weight: bold;
  padding: 0.75rem 2.5rem;
  border-radius: 4px;
  border: 2px solid #9f1a1c;
  transition: all 0.3s ease;
  text-decoration: none;
  font-size: 1.1rem;
  display: inline-block;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  cursor: pointer;
}

.donate-btn:hover {
  background: white;
  color: #9f1a1c;
  transform: translateY(-2px);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
}

.content {
  width: 50%;
  position: relative;
}

.image-container {
  position: relative;
  width: 100%;
  overflow: hidden;
  border-radius: 8px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.15);
}

.image-container img {
  width: 100%;
  height: auto;
  display: block;
  transition: transform 0.5s ease;
}

.image-container:hover img {
  transform: scale(1.03);
}

.decorative-circle {
  position: absolute;
  border-radius: 50%;
  background: rgba(159, 26, 28, 0.1);
  z-index: -1;
}

.decorative-circle.top-right {
  width: 200px;
  height: 200px;
  top: -50px;
  right: -50px;
}

.decorative-circle.bottom-left {
  width: 150px;
  height: 150px;
  bottom: -50px;
  left: -150px;
}

.decorative-line {
  position: absolute;
  height: 3px;
  background: rgba(159, 26, 28, 0);
  width: 150px;
  z-index: -1;
}

.decorative-line.left {
  top: 50%;
  left: -75px;
  transform: translateY(-50%);
}

.banner-section {
  width: 100%;
  /* margin: 3rem 0; */
  margin-top: 3rem;
  position: relative;
}

.banner-image {
  width: 100%;
  height: 400px;
  position: relative;
  overflow: hidden;
}

.banner-image img {
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

.second-home {
  width: 100%;
  padding: 5rem 2rem;
  background: #ffffff;
  position: relative;
}

.partners-container {
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
  padding: 2rem;
}

.partners-content {
  text-align: center;
  position: relative;
  z-index: 2;
}

.partners-content .introTe {
  justify-content: center;
  margin-bottom: 2rem;
}

.partners-content p {
  max-width: 800px;
  margin: 0 auto 2rem;
}

.partners-logo-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
  max-width: 1000px;
  margin: 3rem auto 0;
}

.partner-logo-link {
  display: block;
  transition: transform 0.3s ease;
  padding: 1rem;
  border-radius: 8px;
  background: #ffffff;
  box-shadow: 0 10px 10px rgba(0, 0, 0, 0.05);
}

.partner-logo-link:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
}

.partner-logo {
  width: 100%;
  height: auto;
  display: block;
}

.map-container {
  width: 100%;
  padding: 5rem 2rem;
  background: #ff;
}

.map-header {
  text-align: center;
  max-width: 800px;
  margin: 0 auto 3rem;
}

.map-header h1 {
  margin-bottom: 1.5rem;
}

.map-description {
  font-size: 1.2rem;
  color: #333;
}

.map-section {
  max-width: 1200px;
  margin: 0 auto;
  height: 500px;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.15);
}

.map-embed {
  width: 100%;
  height: 700px;
  margin-top: -70px;
  border: none;
}

.core-values-section {
  width: 100%;
  padding: 5rem 2rem;
  background: #ffffff;
  position: relative;
  overflow: hidden;
}

.core-values-section::before {
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

.core-values-header {
  text-align: center;
  max-width: 800px;
  margin: 0 auto 4rem;
}

.core-values-header h1 {
  margin-bottom: 1.5rem;
  position: relative;
  display: inline-block;
}

.core-values-header h1::after {
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

.value-cards-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.value-card {
  background: #9f1a1c;
  color: white;
  border-radius: 10px;
  padding: 2.5rem 1.5rem;
  text-align: center;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
  transition:
    transform 0.3s ease,
    box-shadow 0.3s ease;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.value-card:hover {
  transform: translateY(-10px) rotate3d(1, 1, 0, 5deg);
  box-shadow: 0 16px 30px rgba(0, 0, 0, 0.15);
}

.first-part {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 1.5rem;
}

.first-part img {
  width: 64px;
  height: 64px;
  margin-bottom: 1rem;
}

.first-part h2 {
  font-size: 1.8rem;
  font-weight: bold;
  margin: 0;
}

.value-card p {
  color: white;
  font-size: 1.1rem;
  line-height: 1.6;
  margin: 0;
}

.values-carousel {
  max-width: 500px;
  margin: 0 auto;
  position: relative;
  padding: 0 1rem;
  touch-action: pan-x;
}

.value-slide {
  background: #9f1a1c;
  color: white;
  border-radius: 10px;
  padding: 2.5rem 1.5rem;
  text-align: center;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
  min-height: 350px;
}

.value-slide p {
  color: white;
}

.value-indicators {
  display: flex;
  justify-content: center;
  margin-top: 1.5rem;
}

.value-indicators span {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: rgba(159, 26, 28, 0.3);
  margin: 0 5px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.value-indicators span.active {
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
  .first-home {
    padding: 4rem 2rem;
  }

  h1 {
    font-size: 3rem;
  }

  .value-cards-container {
    grid-template-columns: repeat(2, 1fr);
  }

  .partners-logo-grid {
    grid-template-columns: repeat(4, 1fr);
    gap: 1.5rem;
  }
}

@media (max-width: 992px) {
  .introTe {
    margin-top: 20%;
  }

  .first-home {
    flex-direction: column;
    padding: 3rem 2rem;
  }

  .hero,
  .content {
    width: 100%;
    padding: 0;
  }

  .hero {
    margin-bottom: 3rem;
  }

  .intro-text-wrapper {
    align-items: center;
    text-align: center;
  }

  .introTe {
    justify-content: center;
  }

  .button-wrapper {
    display: flex;
    justify-content: center;
  }

  .partners-container {
    padding: 1rem;
  }

  .partners-content p {
    width: 90%;
  }

  .banner-image {
    height: 300px;
  }

  .core-values-header h1 {
    font-size: 2.5rem;
  }

  .partners-logo-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (max-width: 768px) {
  h1 {
    font-size: 2.5rem;
  }

  p {
    font-size: 1.1rem;
  }

  .desktop-only {
    display: none;
  }

  .mobile-only {
    display: block;
  }

  .first-home {
    padding: 2rem 1rem;
  }

  .second-home {
    padding: 3rem 1rem;
  }

  .map-container {
    padding: 3rem 1rem;
  }

  .core-values-section {
    padding: 3rem 1rem;
  }

  .decorative-circle,
  .decorative-line {
    opacity: 0.5;
    transform: scale(0.7);
  }

  .banner-image {
    height: 250px;
  }

  .map-section {
    height: 400px;
  }

  .map-embed {
    height: 600px;
    margin-top: -70px;
  }

  .partners-logo-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  h1 {
    font-size: 2rem;
  }

  p {
    font-size: 1rem;
  }

  .donate-btn {
    padding: 0.6rem 1.8rem;
    font-size: 1rem;
  }

  .banner-image {
    height: 200px;
  }

  .first-part h2 {
    font-size: 1.5rem;
  }

  .value-card p,
  .value-slide p {
    font-size: 1rem;
  }

  .map-section {
    height: 350px;
  }

  .map-embed {
    height: 550px;
    margin-top: -70px;
  }

  .partners-logo-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>
