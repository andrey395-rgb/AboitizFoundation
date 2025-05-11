<script setup lang="ts"></script>

<template>
  <div class="home">
    <div class="first-home">
      <section class="hero">
        <div class="intro-text-wrapper">
          <div class="introTe">
            <h1 style="color: black">Who <span style="color: #9f1a1c">We Are</span></h1>
          </div>

          <p>
            The Aboitiz Group's commitment to giving back traces its roots over a century ago. This
            legacy has been instilled and passed on through generations of its corporate history,
            with the help of our partners.
          </p>
          <div class="donate-wrapper">
            <a href="#" class="donate-btn">Donate</a>
          </div>
        </div>
      </section>

      <section class="content">
        <img src="/src/components/icons/palestine.svg" alt="kids" />
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
          We partner with the Aboitiz business units. Together with the Aboitiz Business Units, we
          develop and implement CSR projects that aim to co-create safe, empowered, and sustainable
          communities. Tagged as CSR 2.0, our projects deliver long-term benefits, are aligned with
          our core competencies, encourage team member engagement, and are scalable initiatives with
          positive sustainable impact of national scope.
        </p>
        <img src="/src/components/icons/image.svg" style="scale: 0.7" alt="" />
      </div>
    </div>
    <div class="core-values-section">
      <img src="/src/components/icons/groupaboitiz.png" alt="" />
      <div class="core-values-header">
        <h1 style="color: #000000">
          The Aboitiz Way: <span style="color: #9f1a1c">Our Core Values</span>
        </h1>
        <p>
          For over a hundred years of doing business, we in the Aboitiz Group have nurtured and
          strengthened our core values and beliefs that guide us to be the best at what we do, and
          embolden us to uphold our mission of creating long-term value for all our stakeholders.
        </p>
      </div>
      <div class="value-cards-container">
        <div class="first-card-container">
          <div class="value-card">
            <h2>INTEGRITY</h2>
            <p>
              We believe in integrity. We deliver on what we promise, practice fair processes, are
              accountable for our actions and their consequences.
            </p>
          </div>
          <div class="value-card">
            <h2>TEAMWORK</h2>
            <p>
              We believe in teamwork. We apply a multi-disciplinary approach to achieve our business
              goals. We work independently while promoting cooperation and mutual respect.
            </p>
          </div>
        </div>
        <div class="second-card-container">
          <div class="value-card">
            <h2>INNOVATION</h2>
            <p>
              We believe in innovation. We constantly look for better ways to provide efficient
              systems, quality service and products.
            </p>
          </div>
          <div class="value-card">
            <h2>RESPONSIBILITY</h2>
            <p>
              We believe in responsibility. We adhere to good corporate governance, advocate
              organizational and environmental sustainability, and care for all our stakeholders.
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.core-values-section {
  width: 100%;
  padding: 0;
  /* background: #9f1a1c; */
  display: flex;
  justify-content: center;
  flex-direction: column;
  color: white;
  margin-bottom: 5rem;
}
.core-values-header {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  margin: 2rem 0 2rem 0;
  h1 {
    margin-bottom: 1rem;
  }
  p {
    max-width: 50%;
    color: #000000;
  }
}
.value-cards-container {
  display: flex;
  flex-direction: row;
  align-items: first baseline;
  justify-content: center;
  gap: 0.75rem;
  width: 100%;
  text-align: center;
  .value-card {
    width: 400px;
    /* height: 200px; */
    background: #9f1a1c;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    align-items: left;
    text-align: left;
    /* justify-content: center; */
    padding: 4rem;
    color: white;
    margin-bottom: 1rem;
    box-shadow: 0 8px 8px rgba(0, 0, 0, 0.1);
    transition:
      transform 0.3s,
      box-shadow 0.3s;
    p {
      color: white;
    }
  }
  .value-card:hover {
    transform: rotate3d(1, 1, 0, 10deg) scale(1.07);
    box-shadow: 0 16px 24px rgba(0, 0, 0, 0.15);
  }
}
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

.donate-btn {
  background: #dc1b28;
  color: white;
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
  margin-top: 5rem;

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

/* .donate-btn {
  background: #dc1b28;
  color: white;
  padding: 0.5rem 1.5rem;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.donate-btn:hover {
  background: #b01520;
} */

.vmgo-section {
  width: 100%;
  padding: 4rem 2rem;
  background: #9f1a1c;
  display: flex;
  justify-content: center;
  align-items: center;
}

.vmgo-container {
  max-width: 1200px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  gap: 2rem;
}

.vision-card,
.mission-card,
.goal-card {
  flex: 1;
  background: rgba(255, 255, 255, 0.1);
  padding: 2rem;
  border-radius: 8px;
  text-align: center;
  transition: transform 0.3s ease;
}

.vision-card:hover,
.mission-card:hover,
.goal-card:hover {
  transform: translateY(-5px);
}

.vision-card h2,
.mission-card h2,
.goal-card h2 {
  color: #ffffff;
  font-size: 2rem;
  margin-bottom: 1rem;
}

.vision-card p,
.mission-card p,
.goal-card p {
  color: #ffffff;
  font-size: 1.1rem;
  line-height: 1.6;
  margin: 0;
  width: 100%;
}
</style>
