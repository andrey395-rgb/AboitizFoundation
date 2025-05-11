<template>
  <div class="schedule-container">
    <!-- <h1>Schedule a Meeting</h1> -->
    <div class="calendly-container">
      <div
        class="calendly-inline-widget"
        data-url="https://calendly.com/aboitizfoundation211/30min?primary_color=dc1b28"
      ></div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted } from 'vue'

onMounted(() => {
  // Load Calendly script
  const script = document.createElement('script')
  script.src = 'https://assets.calendly.com/assets/external/widget.js'
  script.async = true
  document.head.appendChild(script)
})
</script>

<style scoped>
.schedule-container {
  width: 100%;
  min-height: 100vh;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: #ffffff;
  margin-top: 7vh;
}

.schedule-container h1 {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: 0rem;
}

.calendly-container {
  width: 100%;
  max-width: 1400px;
  margin-top: 1rem;
  display: flex;
  justify-content: center;
}

.calendly-inline-widget {
  width: 100%;
  height: 700px;
  min-width: 800px;
}
</style>
