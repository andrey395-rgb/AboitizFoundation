<template>
  <nav class="navbar">
    <div class="nav-container">
      <div class="logo">
        <img
          src="./icons/Logo.png"
          alt="Aboitiz Foundation"
        />
      </div>

      <div class="nav-center">
        <router-link to="/">Home</router-link>
        <router-link to="/services">Services</router-link>
        <router-link to="/gallery">Gallery</router-link>
        <router-link to="/scheduling">Scheduling</router-link>
        <router-link to="/contact">Contact Us</router-link>
      </div>

      <div class="nav-right">
        <a href="#" class="donate-btn">Donate</a>
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
// Component logic here if needed
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

</style>
