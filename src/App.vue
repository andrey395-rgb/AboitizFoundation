<script setup lang="ts">
import { RouterView, useRoute } from 'vue-router'
import NavBar from './components/NavBar.vue'
import Footer from './components/Footer.vue'
import { computed } from 'vue'

const route = useRoute()

// Example: Hide navbar on login page
const showNavbar = computed(() => route.name !== 'login')
// Example: Hide footer on specific pages
const showFooter = computed(() => !['login', 'register'].includes(route.name as string))
</script>

<template>
  <div class="app">
    <NavBar />
    <main class="main-content">
      <router-view></router-view>
    </main>
    <Footer />
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html,
body,
#app {
  margin: 0;
  padding: 0;
  width: 100vw;
  min-width: 100vw;
  overflow-x: hidden;
  font-family: Arial, sans-serif;
  line-height: 1.6;
}

.app {
  min-height: 100vh;
  width: 100vw;
  min-width: 100vw;
  display: flex;
  flex-direction: column;
  margin: 0;
  padding: 0;
  overflow-x: hidden;
  position: relative;
  background-color: #ffffff;
}

.main-content {
  flex: 1;
  width: 100vw;
  min-width: 100vw;
  padding: 0;
  box-sizing: border-box;
  background-color: #ffffff;
  color: #000;
}
</style>
