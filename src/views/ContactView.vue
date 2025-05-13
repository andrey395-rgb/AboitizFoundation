<template>
  <div class="home">
    <div class="first-home">
      <div class="left-container">
        <h1 id="contactus-label" style="font-weight: bold">Contact Us</h1>
        <h2 style="color: #dc1b28">Reach and Contact us for a future that's brighter than ever</h2>

        <h2 class="map-label" style="font-weight: bold">Main Office</h2>
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d6494.815107797587!2d121.04721946907354!3d14.55113101150897!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3397c8f3ef7d91c1%3A0x4f126248847ee7c!2sNAC%20Tower%2C%2032nd%20St%2C%20Taguig%2C%20Metro%20Manila!5e0!3m2!1sen!2sph!4v1746863152090!5m2!1sen!2sph"
          width="600"
          height="300"
          style="border: 0"
          loading="lazy"
          referrerpolicy="no-referrer-when-downgrade"
        ></iframe>
        <div class="callus-container">
          <h1 style="font-weight: bold">Call Us</h1>
          <div class="inner-icons">
            <img src="/src/components/icons/call.png" alt="" />
            <h2>Tel: (63 2) 8886 2800 loc 12666</h2>
          </div>
        </div>
        <div class="visitus-container">
          <div class="inner-icons"></div>
        </div>
      </div>
      <div class="right-container">
        <section id="contact">
          <!-- <h1 class="sectionTitle">Work with me!</h1> -->
          <form action="https://formspree.io/f/mqaqbzvl" method="POST">
            <div class="formGroup">
              <label class="label-for-input" for="name" style="color: white"> Name </label> <br />
              <input
                type="text"
                name="name"
                id="name"
                style="width: 45vh; border-radius: 1vh; padding: 1vh; border-style: none"
                required
              />
            </div>
            <div class="formGroup">
              <label class="label-for-input" for="email" style="color: white"> Email </label> <br />
              <input
                type="text"
                name="email"
                id="email"
                style="width: 45vh; border-radius: 1vh; padding: 1vh; border-style: none"
                required
              />
            </div>
            <div class="formGroup">
              <label class="label-for-input" for="message" style="color: white"> Message </label>
              <br />
              <textarea
                name="message"
                id="message"
                style="
                  width: 45vh;
                  min-height: 30vh;
                  max-width: 45vh;
                  padding: 1vh;
                  border-radius: 1vh;
                  border-style: none;
                "
                required
              ></textarea>
            </div>
            <input class="hover-btn" type="submit" value="Submit" />
          </form>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ContactView',
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');
#contactus-label {
  font-size: 4.5vh;
}
.map-label {
  margin-top: 2vh;
}
.callus-container {
  margin-top: 3vh;
  margin-bottom: 3vh;
}
.inner-icons {
  display: flex;
  flex-direction: row;
  align-items: center;
  /* justify-content: center; */
  margin-top: 0.5vh;
  gap: 1rem;
  img {
    width: 4vh;
  }
}
.first-home {
  width: 100%;
  padding: 4rem 4rem 0 4rem;
  display: flex;
  flex-direction: row;
  background: #ffffff;
  align-items: center;
  justify-content: center;
}
.formGroup {
  margin-top: 2vh;
}
.right-container {
  background-color: #dc1b28;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 3vh;
  width: 50%;
  padding: 2rem;
  margin: 0%;
}

.hover-btn {
  padding: 1vh;
  border-radius: 1vh;
  padding: 1vh;
  border-style: none;
  color: #dc1b28;
  background-color: #ffffff;
  transition: all 0.3s ease;
  margin-top: 2vh;
}
.hover-btn:hover {
  scale: 1.05;
  box-shadow: 0 6px 14px rgba(0, 0, 0, 0.178);
}

.left-container {
  width: 50%;
  height: 100%;
  /* padding-top: 10rem; */
  /* gap: 2rem; */
  h2 {
    font-size: 2vh;
  }
  h1 {
    font-size: 2.5vh;
  }
}

.home {
  width: 100%;
  height: 100%;
  padding: 4rem;
  display: flex;
  flex-direction: column;
  background: #ffffff;
  align-items: center;
  justify-content: center;
}

@media (max-width: 1024px) {
  .first-home {
    flex-direction: column;
    padding: 2rem;
  }

  .left-container,
  .right-container {
    width: 100%;
  }

  .right-container {
    margin-top: 2rem;
  }

  input[type='text'],
  textarea {
    width: 100% !important;
    max-width: 100% !important;
  }
}

@media (max-width: 768px) {
  .first-home {
    padding: 1rem;
  }

  .inner-icons {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.5rem;
  }

  .inner-icons img {
    width: 3vh;
  }

  #contactus-label {
    font-size: 3.5vh;
  }
}

@media (max-width: 480px) {
  .first-home {
    padding: 0.5rem;
  }

  .inner-icons img {
    width: 2.5vh;
  }

  #contactus-label {
    font-size: 2.5vh;
  }

  .hover-btn {
    width: 100%;
  }
}
</style>
