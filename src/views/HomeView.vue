<script setup lang="ts">
// Add component logic here
</script>

<template>
  <div class="home">
    <div class="first-home">
      <section class="hero">
        <div class="intro-text-wrapper">
          <div class="introTe">
            <h1 style="color: black">Who <span style="color: #9f1a1c">We Are</span></h1>
          </div>

          <p>
            The Aboitiz Group’s commitment to giving back traces its roots over a century ago. This
            legacy has been instilled and passed on through generations of its corporate history,
            with the help of our partners.
          </p>
          <div class="donate-wrapper">
          <a href="#" class="donate-btn">Donate</a>
        </div>
        </div>


      </section>

      <section class="content">
        <img
          src="/src/components/icons/palestine.svg"
          alt="kids"
        />
        <!-- <h2>Our Mission</h2>
      <p>Add your mission statement here</p> -->
      </section>
    </div>
    <div class="second-home">
      <div class="sponsors-text-wrapper">
          <div class="introTe">
            <h1 style="color: black">Our <span style="color: #9f1a1c">Partners</span></h1>
          </div>

          <p>
            We partner with the Aboitiz business units. Together with the Aboitiz Business Units, we develop and implement CSR projects that aim to co-create safe, empowered, and sustainable communities. Tagged as CSR 2.0, our projects deliver long-term benefits, are aligned with our core competencies, encourage team member engagement, and are scalable initiatives with positive sustainable impact of national scope.
          </p>

          <img src="/src/components/icons/image.svg" style="scale: 0.7;" alt="">
        </div>
    </div>
  </div>
</template>

<style scoped>
.sponsors-text-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.intro-text-wrapper {
  display: flex;
  justify-content: center;

  flex-direction: column;
  margin-top: 1rem;
  padding-left: 15rem;
}
.donate-wrapper {
  display: flex;
  justify-content: left;
  margin-top: 1rem;
}

.first-home {
  width: 100%;
  padding: 0;
  display: flex;
  flex-direction: row;
  background: #ffffff;
  padding-top: 0;
  align-items: center;
  justify-content: center;

  p {
    margin-bottom: 2rem;
    width: 75%;
  }
}
.second-home {
  width: 100%;
  padding: 4rem;
  display: flex;
  flex-direction: row;
  background: #ffffff;
  padding-top: 0;
  align-items: center;
  justify-content: center;

  p {
    margin-bottom: 2rem;
    width: 75%;

  }
}
.home {
  width: 100%;
  padding: 0;
  display: flex;
  flex-direction: column;
  background: #ffffff;
  padding-top: 0;
  align-items: center;
  justify-content: center;

  p {
    margin-bottom: 2rem;
    width: 75%;
  }
}

.hero {
  padding: 4rem 2rem;
  gap: 20rem;
  width: 50%;
  background: #ffffff;
}

.content {
  max-width: 1200px;
  padding: 0 0;
  background: #ffffff;
  width: 50%;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  img {
    width: 91.5%;
    height: auto;
  }
}

.introTe {
  display: flex;
  flex-direction: row;
  justify-content: left;
  align-items: center;
  text-align: center;
  gap: 0.5rem;
  p {
    font-size: 47px;
  }
  h1 {
    font-size: 62px;
  }
}

.donate-btn {
  background: #dc1b28;
  color: white;
  padding: 0.5rem 1.5rem;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.donate-btn:hover {
  background: #b01520;
}
</style>
