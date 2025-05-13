<template>
  <nav class="navbar" :class="{ 'navbar-hidden': isHidden }">
    <div class="nav-container">
      <div class="logo">
        <img src="./icons/Logo.png" alt="Aboitiz Foundation" />
      </div>

      <!-- Desktop Navigation -->
      <div class="nav-center">
        <router-link to="/">Home</router-link>
        <router-link to="/services">Services</router-link>
        <router-link to="/gallery">Gallery</router-link>
        <router-link to="/schedule">Scheduling</router-link>
        <router-link to="/contact">Contact Us</router-link>
      </div>

      <div class="nav-right">
        <a href="#" class="donate-btn">Donate</a>
        <button
          class="hamburger-btn"
          @click="toggleMobileMenu"
          aria-label="Toggle navigation menu"
        >
          <div class="hamburger" :class="{ 'active': isMobileMenuOpen }">
            <span></span>
            <span></span>
            <span></span>
          </div>
        </button>
      </div>
    </div>

    <!-- Mobile Navigation -->
    <div class="mobile-menu" :class="{ 'open': isMobileMenuOpen }">
      <router-link to="/" @click="closeMobileMenu">Home</router-link>
      <router-link to="/services" @click="closeMobileMenu">Services</router-link>
      <router-link to="/gallery" @click="closeMobileMenu">Gallery</router-link>
      <router-link to="/schedule" @click="closeMobileMenu">Scheduling</router-link>
      <router-link to="/contact" @click="closeMobileMenu">Contact Us</router-link>
      <a href="#" class="mobile-donate-btn" @click="closeMobileMenu">Donate</a>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

const isMobileMenuOpen = ref(false);
const isHidden = ref(false);
const lastScrollY = ref(0);
const scrollThreshold = 50; // Minimum scroll amount before showing/hiding

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value;

  // Prevent body scrolling when menu is open
  if (isMobileMenuOpen.value) {
    document.body.style.overflow = 'hidden';
  } else {
    document.body.style.overflow = '';
  }
};

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false;
  document.body.style.overflow = '';
};

const handleScroll = () => {
  const currentScrollY = window.scrollY;

  // Don't hide navbar at the very top of the page
  if (currentScrollY < 10) {
    isHidden.value = false;
    lastScrollY.value = currentScrollY;
    return;
  }

  // Determine scroll direction and distance
  if (currentScrollY > lastScrollY.value + scrollThreshold) {
    // Scrolling down
    isHidden.value = true;
  } else if (currentScrollY < lastScrollY.value - 10) {
    // Scrolling up (more sensitive to show the navbar)
    isHidden.value = false;
  }

  lastScrollY.value = currentScrollY;
};

// Handle window resize to close mobile menu on larger screens
const handleResize = () => {
  if (window.innerWidth > 768 && isMobileMenuOpen.value) {
    closeMobileMenu();
  }
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
  window.addEventListener('resize', handleResize);
  lastScrollY.value = window.scrollY;
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
  window.removeEventListener('resize', handleResize);
});
</script>

<style scoped>
.navbar {
  width: 100%;
  background: white;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.navbar-hidden {
  transform: translateY(-100%);
  box-shadow: none;
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
  max-height: 60px;
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
  background-color: transparent;
}

.nav-center a:hover::after {
  transform: scaleX(1);
}

.nav-right {
  flex: 1;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 1rem;
}

.donate-btn {
  background: #dc1b28;
  color: white !important;
  font-weight: bold;
  padding: 0.5rem 1.5rem;
  border-radius: 4px;
  border: 2px solid #dc1b28;
  transition: all 0.3s ease;
  text-decoration: none;
}

.donate-btn:hover {
  background: white;
  color: #dc1b28 !important;
  box-shadow: 0 6px 14px rgba(0, 0, 0, 0.178);
}

/* Hamburger Menu Styles */
.hamburger-btn {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: 10px;
  margin-left: 10px;
}

.hamburger {
  width: 24px;
  height: 20px;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.hamburger span {
  display: block;
  height: 3px;
  width: 100%;
  background-color: #333;
  border-radius: 3px;
  transition: all 0.3s ease;
}

.hamburger.active span:nth-child(1) {
  transform: translateY(8.5px) rotate(45deg);
}

.hamburger.active span:nth-child(2) {
  opacity: 0;
}

.hamburger.active span:nth-child(3) {
  transform: translateY(-8.5px) rotate(-45deg);
}

/* Mobile Menu */
.mobile-menu {
  position: fixed;
  top: 50px; /* Height of navbar */
  left: 0;
  width: 100%;
  background: white;
  flex-direction: column;

  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transform: translateY(-100%);
  opacity: 0;
  visibility: hidden;
  transition: transform 0.3s ease, opacity 0.3s ease, visibility 0.3s ease;
  z-index: 999;
  max-height: calc(100vh - 70px);
  overflow-y: auto;
}

.mobile-menu.open {
  transform: translateY(0);
  opacity: 1;
  visibility: visible;
}

.mobile-menu a {
  padding: 1rem 2rem;
  text-decoration: none;
  color: #333;
  font-weight: bold;
  border-bottom: 1px solid #eee;
  transition: background-color 0.3s ease;
  display: block;
}

.mobile-menu a:hover,
.mobile-menu a:active {
  background-color: #f5f5f5;
  color: #dc1b28;
}

.mobile-donate-btn {

  background: #dc1b28;
  color: white !important;
  font-weight: bold;
  padding: 0.75rem;



  transition: all 0.3s ease;
}

.mobile-donate-btn:hover {
  background: white;
  color: #dc1b28 !important;
}

/* Media Queries */
@media (max-width: 1100px) {
  .nav-center {
    display: none;
  }

  .donate-btn {
    display: none;
  }

  .hamburger-btn {
    display: block;
  }

  .mobile-menu {
    display: flex;
  }

  .nav-container {
    padding: 0.5rem 1rem;
  }

  .logo {
    flex: 0;
  }

  .logo img {
    height: 6vh;
    max-height: 50px;
  }

  .nav-right {
    flex: 0;
  }
}

/* For very small screens */
@media (max-width: 480px) {
  .logo img {
    height: 5vh;
    max-height: 40px;
  }

  .nav-container {
    padding: 0.5rem 0.75rem;
  }
}
</style>
