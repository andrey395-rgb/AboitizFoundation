<template>
  <nav class="navbar">
    <div class="nav-container">
      <div class="logo">
        <img src="./icons/Logo.png" alt="Aboitiz Foundation" />
      </div>

      <div class="burger-menu" @click="toggleMenu">
        <div class="bar" :class="{ active: isMenuOpen }"></div>
        <div class="bar" :class="{ active: isMenuOpen }"></div>
        <div class="bar" :class="{ active: isMenuOpen }"></div>
      </div>

      <div class="nav-center" :class="{ active: isMenuOpen }">
        <router-link to="/" @click="closeMenu">Home</router-link>
        <router-link to="/services" @click="closeMenu">Services</router-link>
        <router-link to="/gallery" @click="closeMenu">Gallery</router-link>
        <router-link to="/schedule" @click="closeMenu">Scheduling</router-link>
        <router-link to="/contact" @click="closeMenu">Contact Us</router-link>
      </div>

      <div class="nav-right" :class="{ active: isMenuOpen }">
        <a href="#" class="donate-btn">Donate</a>
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const isMenuOpen = ref(false)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}
</script>

<style scoped>
.navbar {
  width: 100vw;
  background: white;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
}

.nav-container {
  width: 100%;
  max-width: 1440px;
  margin: 0 auto;
  padding: 0.5rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  flex: 1;
  display: flex;
  justify-content: flex-start;
}

.logo img {
  height: 7vh;
}

.burger-menu {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 30px;
  height: 21px;
  cursor: pointer;
  z-index: 1001;
}

.bar {
  width: 100%;
  height: 3px;
  background-color: #333;
  transition: all 0.3s ease;
}

.bar.active:nth-child(1) {
  transform: translateY(9px) rotate(45deg);
}

.bar.active:nth-child(2) {
  opacity: 0;
}

.bar.active:nth-child(3) {
  transform: translateY(-9px) rotate(-45deg);
}

.nav-center {
  flex: 2;
  display: flex;
  justify-content: center;
  gap: 2rem;
  align-items: center;
}

.nav-center a {
  text-decoration: none;
  color: #333;
  font-weight: bold;
  position: relative;
  transition: color 0.3s ease;
  background-color: transparent;
  -webkit-tap-highlight-color: transparent;
}

.nav-center a::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: -4px;
  width: 100%;
  height: 2px;
  background-color: #dc1b28;
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.3s ease;
}

.nav-center a:hover {
  color: #dc1b28;
  background-color: transparent; /* Prevent any background flash */
}

.nav-center a:hover::after {
  transform: scaleX(1);
}

.nav-right {
  flex: 1;
  display: flex;
  justify-content: flex-end;
}

.donate-btn {
  background: #dc1b28;
  color: white !important;
  font-weight: bold;
  padding: 0.5rem 1.5rem;
  border-radius: 4px;
  border: 2px solid #dc1b28;
  transition: all 0.3s ease;
}

.donate-btn:hover {
  background: white;
  color: #dc1b28 !important;
  box-shadow: 0 6px 14px rgba(0, 0, 0, 0.178);
}

@media (max-width: 829px) {
  .burger-menu {
    display: flex;
  }

  .nav-center {
    position: fixed;
    top: 0;
    right: -100%;
    width: 70%;
    height: 100vh;
    background: white;
    flex-direction: column;
    padding: 80px 20px;
    transition: right 0.3s ease;
    box-shadow: -2px 0 5px rgba(0, 0, 0, 0.1);
  }

  .nav-center.active {
    right: 0;
  }

  .nav-right {
    position: fixed;
    top: 70%;
    right: -100%;
    width: 70%;
    padding: 20px;
    transition: right 0.3s ease;
  }

  .nav-right.active {
    right: 0;
  }

  .nav-center a {
    margin: 15px 0;
    font-size: 1.2rem;
  }

  .logo img {
    height: 5vh;
  }
}

@media (max-width: 480px) {
  .nav-center {
    width: 100%;
  }

  .nav-right {
    width: 100%;
  }
}
</style>
