<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

const galleryRows = ref(4);

const galleryItems = [
  { id: 1, title: "Education Initiative", description: "Providing schools and learning materials to underprivileged communities.", image: "/src/components/icons/s1.png" },
  { id: 2, title: "Medical Camp", description: "Free health checkups and medicines in rural areas.", image: "/src/components/icons/s2.png" },
  { id: 3, title: "Food Distribution", description: "Ensuring no family goes hungry in our partner communities.", image: "/src/components/icons/s3.png" },
  { id: 4, title: "Environmental Program", description: "Tree planting and conservation efforts.", image: "/src/components/icons/s4.png" },
  { id: 5, title: "Shelter Project", description: "Building homes for displaced families.", image: "/src/components/icons/s5.png" },
  { id: 6, title: "Livelihood Training", description: "Skills development for sustainable income.", image: "/src/components/icons/s6.png" },
];

const duplicatedItems = [...galleryItems, ...galleryItems];


const getAnimationDuration = () => {
  const baseDuration = 40;
  return `${baseDuration}s`;
};

const stats = [
  { value: 7845, label: "Lives Positively Impacted", suffix: "+" },
  { value: 412, label: "Community Projects Completed", suffix: "" },
  { value: 86, label: "Partner Organizations", suffix: "" },
  { value: 1.8, label: "Billion Pesos Invested in Communities", prefix: "₱", suffix: "B" }
];

const animatedStats = ref(stats.map(stat => ({
  ...stat,
  current: 0
})));

const startCountingStats = () => {
  const duration = 2000;
  const frameDuration = 1000 / 60;
  const totalFrames = Math.round(duration / frameDuration);

  let frame = 0;
  const countUp = () => {
    const progress = frame / totalFrames;
    const easeProgress = progress === 1 ? 1 : 1 - Math.pow(2, -10 * progress);

    animatedStats.value = stats.map((stat, index) => ({
      ...stat,
      current: Math.floor(easeProgress * stat.value)
    }));

    frame++;

    if (frame <= totalFrames) {
      requestAnimationFrame(countUp);
    }
  };

  requestAnimationFrame(countUp);
};

const statsObserver = ref(null);
const statsSection = ref(null);

onMounted(() => {
  statsObserver.value = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        startCountingStats();
        statsObserver.value.disconnect();
      }
    });
  }, { threshold: 0.2 });

  if (statsSection.value) {
    statsObserver.value.observe(statsSection.value);
  }
});

onUnmounted(() => {
  if (statsObserver.value) {
    statsObserver.value.disconnect();
  }
});

const observeElements = () => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.fade-in').forEach(el => {
    observer.observe(el);
  });
};

onMounted(() => {
  observeElements();
});
</script>

<template>
  <div class="gallery-container">
    <section class="header-section">
      <div class="header-content">
        <h1><span class="normal">Our</span> <span class="accent">Works</span></h1>
        <p>
          As our strategies continue to evolve through integration, we also continuously improve our implementing structures.
          We see the critical role of collaboration and a sustainable approach towards advancing communities.
        </p>
      </div>
    </section>

    <section class="gallery-section">
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
              :src="item.image"
              :alt="item.title"
              class="gallery-image"
            />
            <div class="gallery-overlay">
              <h3>{{ item.title }}</h3>
              <p>{{ item.description }}</p>
            </div>
          </div>
        </div>

        <div class="gallery-track" aria-hidden="true">
          <div
            v-for="(item, index) in duplicatedItems"
            :key="`${row}-${index}-mirror`"
            class="gallery-item"
          >
            <img
              :src="item.image"
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
    </section>


    <section ref="statsSection" class="stats-section fade-in">
      <div class="stats-container">
        <div class="stats-header">
          <h2>Transforming <span class="accent">Communities</span> Together</h2>
          <p>
            Our nationwide presence enables us to create meaningful impact where it matters most.
            Through our Vision 2030 initiative, we're committed to building resilient,
            sustainable communities across the Philippines.
          </p>
        </div>

        <div class="stats-grid">
          <div v-for="(stat, index) in animatedStats" :key="index" class="stat-card">
            <div class="stat-value">
              <span v-if="stat.prefix">{{ stat.prefix }}</span>{{ stat.current.toLocaleString() }}<span v-if="stat.suffix" class="suffix">{{ stat.suffix }}</span>
            </div>
            <div class="stat-label">{{ stat.label }}</div>
            <div class="stat-underline"></div>
          </div>
        </div>

        <div class="stats-cta">
          <a href="/contact" class="cta-button">Join Our Mission</a>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.gallery-container {
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
  margin-bottom: 1.5rem;
}

h1 .normal {
  color: #000000;
}

h1 .accent {
  color: #9f1a1c;
}

h2 {
  font-size: 3rem;
  font-weight: bold;
  line-height: 1.2;
  margin-bottom: 1.5rem;
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
  transition: opacity 0.8s ease, transform 0.8s ease;
}

.fade-in.visible {
  opacity: 1;
  transform: translateY(0);
}

.header-section {
  padding: 5rem 2rem 3rem;
  text-align: center;
}

.header-content {
  max-width: 800px;
  margin: 0 auto;
}

.gallery-section {
  width: 100%;
  padding: 2rem 0 3rem;
  background: #ffffff;
  overflow: hidden;
}

.gallery-row {
  display: flex;
  width: 100%;
  overflow: hidden;
  position: relative;
  margin-bottom: 1rem;
  margin-left: 1rem;

}

.gallery-track {
  display: flex;
  animation: scroll var(--animation-duration) linear infinite;
  animation-direction: var(--direction);
  will-change: transform;
  margin-right: 1rem;
}

.gallery-row:hover .gallery-track {
  animation-play-state: paused;
}

@keyframes scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-100%);
  }
}

.gallery-item {
  position: relative;
  min-width: 300px;
  height: 200px;
  flex-shrink: 0;
  transition: all 0.3s ease;
  overflow: hidden;
  margin: 0 0.5rem;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
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
  padding: 1.5rem;
  opacity: 0;
  transition: opacity 0.3s ease;
  text-align: center;
}

.gallery-overlay h3 {
  font-size: 1.5rem;
  margin-bottom: 0.75rem;
  font-weight: 600;
}

.gallery-overlay p {
  font-size: 1rem;
  color: white;
  line-height: 1.5;
  margin: 0;
}

.gallery-item:hover .gallery-overlay {
  opacity: 1;
}

.gallery-item:hover .gallery-image {
  transform: scale(1.1);
}

.stats-section {
  width: 100%;
  padding: 5rem 2rem;
  background: #f5f5f5;
  position: relative;
  overflow: hidden;
}

.stats-section::before {
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

.stats-container {
  max-width: 1200px;
  margin: 0 auto;
}

.stats-header {
  text-align: center;
  max-width: 800px;
  margin: 0 auto 4rem;
}

.stats-header h2 {
  position: relative;
  display: inline-block;
}

.stats-header h2::after {
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

.stats-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
  margin-bottom: 3rem;
}

.stat-card {
  text-align: center;
  padding: 2rem 1rem;
  background: white;
  border-radius: 8px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  position: relative;
  overflow: hidden;
}

.stat-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 4px;
  height: 100%;
  background: #9f1a1c;
}

.stat-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.12);
}

.stat-value {
  font-size: 3.5rem;
  font-weight: 800;
  color: #9f1a1c;
  line-height: 1;
  margin-bottom: 1rem;
}

.stat-value .suffix {
  font-weight: 800;
}

.stat-label {
  font-size: 1.2rem;
  font-weight: 600;
  color: #333;
  line-height: 1.4;
}

.stat-underline {
  width: 40px;
  height: 3px;
  background: #9f1a1c;
  margin: 1rem auto 0;
}

.stats-cta {
  text-align: center;
  margin-top: 3rem;
}

.cta-button {
  background: #9f1a1c;
  color: white;
  padding: 0.75rem 2.5rem;
  border-radius: 4px;
  transition: all 0.3s ease;
  font-weight: 600;
  text-decoration: none;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  font-size: 1.1rem;
  display: inline-block;
  border: 2px solid #9f1a1c;
}

.cta-button:hover {
  background: white;
  color: #9f1a1c;
  transform: translateY(-2px);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
}


@media (max-width: 1200px) {
  .header-section {
    margin-top: 100px;
  }
  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 1.5rem;
  }

  h1 {
    font-size: 3rem;
  }

  h2 {
    font-size: 2.5rem;
  }
}

@media (max-width: 992px) {
  .gallery-item {
    min-width: 250px;
    height: 180px;
  }
}

@media (max-width: 768px) {
  .header-section {
    padding: 3rem 1.5rem 2rem;
  }

  h1 {
    font-size: 2.5rem;
  }

  h2 {
    font-size: 2rem;
  }

  p {
    font-size: 1.1rem;
  }

  .gallery-section {
    padding: 2rem 0;
  }

  .gallery-item {
    min-width: 200px;
    height: 150px;
  }

  .gallery-overlay h3 {
    font-size: 1.2rem;
    margin-bottom: 0.5rem;
  }

  .gallery-overlay p {
    font-size: 0.9rem;
  }

  .stats-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .stat-value {
    font-size: 3rem;
  }

  .stat-label {
    font-size: 1.1rem;
  }

  .stats-section {
    padding: 3rem 1.5rem;
  }

  .stats-header {
    margin-bottom: 2.5rem;
  }
}

@media (max-width: 480px) {
  .header-section {
    padding: 2.5rem 1rem 1.5rem;
  }

  h1 {
    font-size: 2rem;
  }

  h2 {
    font-size: 1.8rem;
  }

  p {
    font-size: 1rem;
  }

  .gallery-item {
    min-width: 150px;
    height: 120px;
  }

  .gallery-overlay h3 {
    font-size: 1rem;
    margin-bottom: 0.25rem;
  }

  .gallery-overlay p {
    font-size: 0.8rem;
  }

  .stat-value {
    font-size: 2.5rem;
  }

  .stat-label {
    font-size: 1rem;
  }

  .cta-button {
    padding: 0.6rem 1.8rem;
    font-size: 1rem;
  }
}
</style>
