<template>
  <div class="schedule-container">
    <h1>Schedule a Meeting</h1>
    <div class="calendly-container">
      <div
        class="calendly-inline-widget"
        data-url="https://calendly.com/natalramirez-addu?primary_color=dc1b28"
        style="min-width: 320px; height: 700px"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ScheduleView',
  mounted() {
    // Load Calendly script
    const script = document.createElement('script')
    script.src = 'https://assets.calendly.com/assets/external/widget.js'
    script.async = true
    document.head.appendChild(script)
  },
}
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
}

.schedule-container h1 {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: 2rem;
}

.calendly-container {
  width: 100%;
  max-width: 1200px;
  margin-top: 2rem;
  display: flex;
  justify-content: center;
}
</style>
