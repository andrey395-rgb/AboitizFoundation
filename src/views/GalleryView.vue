<script setup lang="ts">
import { ref, onMounted } from 'vue';

const galleryRows = ref(4);

// Sample data for gallery items
const galleryItems = [
  { id: 1, title: "Education Initiative", description: "Providing schools and learning materials to underprivileged communities." },
  { id: 2, title: "Medical Camp", description: "Free health checkups and medicines in rural areas." },
  { id: 3, title: "Food Distribution", description: "Ensuring no family goes hungry in our partner communities." },
  { id: 4, title: "Environmental Program", description: "Tree planting and conservation efforts." },
  { id: 5, title: "Shelter Project", description: "Building homes for displaced families." },
  { id: 6, title: "Livelihood Training", description: "Skills development for sustainable income." },
];

// Duplicate items to create seamless infinite scroll
const duplicatedItems = [...galleryItems, ...galleryItems];

// Calculate animation duration based on number of items
const getAnimationDuration = () => {
  const baseDuration = 40; // seconds to complete one full cycle
  return `${baseDuration}s`;
};
</script>

<template>
  <div class="gallery-container">
    <section class="hero">
      <div class="intro-text-wrapper">
        <div class="introTe">
          <h1 style="color: black">Our <span style="color: #9f1a1c">Gallery</span></h1>
        </div>

        <p>
          As our strategies continue to evolve through integration, we also continuously improve our implementing structures.
          We see the critical role of collaboration and a sustainable approach towards advancing communities.
        </p>
      </div>
    </section>

    <div
      v-for="row in galleryRows"
      :key="row"
      class="gallery-row"
      :style="{
        '--animation-duration': getAnimationDuration(),
        '--direction': row % 2 === 0 ? 'reverse' : 'normal'
      }"
    >
      <div class="gallery-track">
        <div
          v-for="(item, index) in duplicatedItems"
          :key="`${row}-${index}`"
          class="gallery-item"
        >
          <img
            src="/src/components/icons/palestine.svg"
            :alt="item.title"
            class="gallery-image"
          />
          <div class="gallery-overlay">
            <h3>{{ item.title }}</h3>
            <p>{{ item.description }}</p>
          </div>
        </div>
      </div>
      <!-- Mirrored track for seamless infinite scroll -->
      <div class="gallery-track" aria-hidden="true">
        <div
          v-for="(item, index) in duplicatedItems"
          :key="`${row}-${index}-mirror`"
          class="gallery-item"
        >
          <img
            src="/src/components/icons/palestine.svg"
            :alt="item.title"
            class="gallery-image"
          />
          <div class="gallery-overlay">
            <h3>{{ item.title }}</h3>
            <p>{{ item.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.gallery-container {
  width: 100%;
  background: #ffffff;
  overflow: hidden;
}

.hero {
  padding: 4rem 2rem;
  display: flex;
  justify-content: center;
  background: #ffffff;
}

.intro-text-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  max-width: 1200px;
  width: 100%;
}

.introTe {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  text-align: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.introTe h1 {
  margin-top: 20%;
  font-size: 62px;
}

.intro-text-wrapper p {
  margin-bottom: 2rem;
  width: 75%;
  max-width: 800px;
}

.gallery-row {
  display: flex;
  width: 100%;
  overflow: hidden;
  position: relative;
}

.gallery-track {
  display: flex;
  animation: scroll var(--animation-duration) linear infinite;
  animation-direction: var(--direction);
  will-change: transform;
}

.gallery-row:hover .gallery-track {
  animation-play-state: paused;
}

@keyframes scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

.gallery-item {
  position: relative;
  min-width: 300px;
  height: 200px;
  flex-shrink: 0;
  transition: all 0.3s ease;
  overflow: hidden;
}

.gallery-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.gallery-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(159, 26, 28, 0.9);
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 1rem;
  opacity: 0;
  transition: opacity 0.3s ease;
  text-align: center;
  white-space: normal;
}

.gallery-overlay h3 {
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
}

.gallery-overlay p {
  font-size: 1rem;
  width: 100%;
}

.gallery-item:hover .gallery-overlay {
  opacity: 1;
}

.gallery-item:hover .gallery-image {
  transform: scale(1.1);
}

/* Mobile responsiveness */
@media (max-width: 1024px) {
  .introTe h1 {
    font-size: 48px;
  }

  .gallery-item {
    min-width: 250px;
    height: 180px;
  }
}

@media (max-width: 768px) {
  .hero {
    padding: 2rem 1rem;
  }

  .introTe h1 {
    font-size: 36px;
  }

  .intro-text-wrapper p {
    width: 90%;
  }

  .gallery-item {
    min-width: 200px;
    height: 150px;
  }
}

@media (max-width: 480px) {
  .gallery-item {
    min-width: 150px;
    height: 120px;
  }

  .gallery-overlay h3 {
    font-size: 1rem;
  }

  .gallery-overlay p {
    font-size: 0.8rem;
  }
}
</style>
