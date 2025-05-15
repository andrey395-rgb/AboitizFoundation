<template>
  <footer class="footer">
    <div class="footer-container">
      <div class="footer-left">
        <img src="./icons/Logo.png" alt="Aboitiz Foundation" class="footer-logo" />
        <div class="address">
          NAC Tower, 32nd Street Bonifacio Global City,<br />
          Taguig City, Philippines
        </div>
        <div class="social-links">
          <a href="#" target="_blank"><i class="fab fa-facebook"></i></a>
          <a href="#" target="_blank"><i class="fab fa-instagram"></i></a>
          <a href="#" target="_blank"><i class="fab fa-linkedin"></i></a>
          <a href="#" target="_blank"><i class="fab fa-youtube"></i></a>
        </div>
      </div>
      <div class="footer-right">
        <div class="partners-logo-grid">
          <a
            v-for="(partner, index) in partners"
            :key="index"
            href="#"
            target="_blank"
            rel="noopener noreferrer"
            class="partner-logo-link"
          >
            <img :src="partner.logo" :alt="partner.name + ' logo'" class="partner-logo" />
          </a>
        </div>
      </div>
    </div>
    <div class="footer-bottom">
      <p>© {{ currentYear }} Copyright Aboitiz Foundation</p>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const currentYear = new Date().getFullYear()

// Partner logos data - matching the HomeView structure
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
</script>

<style scoped>
.footer {
  width: 100%;
  min-width: 100%;
  background: #ffffff;
  padding: 3rem 0 0;
  margin: 0;
  box-sizing: border-box;
  justify-content: center;
  align-items: center;
  border-top: #666 solid 1px;
}

.footer-container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  justify-content: space-between;
  gap: 4rem;
  box-sizing: border-box;
}

.footer-left {
  flex: 1;
  border-right: #666 solid 1px;
  padding-right: 2rem;
}

.footer-logo {
  height: 50px;
  margin-bottom: 1rem;
}

.address {
  color: #666;
  margin-bottom: 1rem;
  line-height: 1.6;
}

.social-links {
  display: flex;
  gap: 1rem;
}

.social-links a {
  color: #666;
  font-size: 1.5rem;
  transition: color 0.3s ease;
}

.social-links a:hover {
  color: #9f1a1c;
}

.footer-right {
  flex: 2;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

/* Partners Logo Grid - 8 logos, matching HomeView */
.partners-logo-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.5rem;
  width: 100%;
}

.partner-logo-link {
  display: block;
  transition: transform 0.3s ease;
  padding: 0.75rem;
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

.footer-bottom {
  width: 100%;
  margin-top: 3rem;
  padding: 1rem 0;
  text-align: center;
  border-top: 1px solid #ddd;
  color: #ffffff;
  box-sizing: border-box;
  background: #9f1a1c;
}

/* Responsive Styles */
@media (max-width: 1200px) {
  .footer-container {
    padding: 0 2rem;
    gap: 3rem;
  }

  .partners-logo-grid {
    grid-template-columns: repeat(4, 1fr);
    gap: 1rem;
  }

  .partner-logo-link {
    padding: 0.5rem;
  }
}

@media (max-width: 992px) {
  .footer-container {
    gap: 2rem;
  }

  .partners-logo-grid {
    grid-template-columns: repeat(3, 1fr);
  }

  .footer-left {
    padding-right: 1.5rem;
  }
}

@media (max-width: 768px) {
  .footer-container {
    flex-direction: column;
    gap: 2rem;
    padding: 0 1.5rem;
  }

  .footer-left {
    width: 100%;
    border-right: none;
    border-bottom: #666 solid 1px;
    padding-right: 0;
    padding-bottom: 2rem;
  }

  .footer-right {
    width: 100%;
    justify-content: flex-start;
  }

  .partners-logo-grid {
    grid-template-columns: repeat(4, 1fr);
    gap: 1rem;
  }
}

@media (max-width: 576px) {
  .partners-logo-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Hide sponsors in mobile view as requested */
@media (max-width: 480px) {
  .footer-right {
    display: none;
  }

  .footer-container {
    padding: 0 1rem;
  }

  .footer-left {
    border-bottom: none;
    padding-bottom: 1rem;
  }

  .footer-logo {
    height: 40px;
  }

  .social-links {
    gap: 0.8rem;
  }

  .social-links a {
    font-size: 1.3rem;
  }

  .address {
    font-size: 0.9rem;
  }

  .footer-bottom {
    margin-top: 1.5rem;
    font-size: 0.9rem;
  }
}
</style>
