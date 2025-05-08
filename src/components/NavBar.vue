<template>
  <nav class="navbar">
    <div class="nav-container">
      <div class="logo">
        <img
          src="./icons/Frame.svg"
          alt="Aboitiz Foundation"
        />
      </div>
      <div class="nav-links">
        <router-link to="/">Home</router-link>
        <router-link to="/services">Services</router-link>
        <router-link to="/gallery">Gallery</router-link>
        <router-link to="/scheduling">Scheduling</router-link>
        <router-link to="/contact">Contact Us</router-link>
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
  opacity: 0.8;
}

.nav-container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo img {
  height: 7vh;
}

.nav-links {
  display: flex;
  gap: 2rem;
  align-items: center;
}

.nav-links a {
  text-decoration: none;
  color: #333;
  font-weight: 500;
  transition: color 0.3s ease;
}

.nav-links a:hover {
  color: #dc1b28;
}

.donate-btn {
  background: #dc1b28;
  color: white !important;
  padding: 0.5rem 1.5rem;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.donate-btn:hover {
  background: #b01520;
}
</style>
