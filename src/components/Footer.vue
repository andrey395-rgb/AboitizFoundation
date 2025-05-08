<template>
  <footer class="footer">
    <div class="footer-container">
      <div class="footer-left">
        <img
          src="./icons/Frame.svg"
          alt="Aboitiz Foundation"
          class="footer-logo"
        />
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
        <div class="partner-logos">
          <div class="first-row">
            <img
              src="./icons/image.svg"
              alt="Aboitiz Construction"
            />
          </div>
        </div>
      </div>
    </div>
    <div class="footer-bottom">
      <p>© {{ currentYear }} Copyright Aboitiz Foundation</p>
    </div>
  </footer>
</template>

<script setup lang="ts">
const currentYear = new Date().getFullYear()
</script>

<style scoped>
.footer {
  width: 100%;
  min-width: 100%;
  background: #FFFFFF;
  padding: 3rem 0 0;
  margin: 0 0 0 0;
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
  gap: 15rem;
  box-sizing: border-box;
  /* border-top: #666 solid 1px; */
}

.footer-left {
  flex: 1;
  border-right: #666 solid 1px;
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
  color: #dc1b28;
}

.footer-right {
  flex: 2;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.partner-logos {
  display: flex;
  justify-content: flex-end;
  width: 100%;

  .first-row {
    display: flex;
    gap: 2rem;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: flex-end;
    width: 100%;
  }
  .second-row {
    display: flex;
    gap: 2rem;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: flex-end;
    width: 100%;
  }
}

.partner-logos img {
  max-width: 100%;
  height: auto;
 
}

.partner-logos img:hover {
  filter: grayscale(0%);
}

.footer-bottom {
  width: 100%;
  margin-top: 3rem;
  padding: 1rem 0;
  text-align: center;
  border-top: 1px solid #ddd;
  color: #666;
  box-sizing: border-box;
  background: #9f1a1c;
  color: white;
}

@media (max-width: 768px) {
  .footer-container {
    flex-direction: column;
  }

  .partner-logos {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>
