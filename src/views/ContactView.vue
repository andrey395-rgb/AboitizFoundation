<template>
  <div class="home">
    <div class="first-home">
      <div class="message-container">
        <h1>Location Map</h1>
        <iframe
          src="https://www.google.com/maps/d/embed?mid=19M5SYCrApuPKYSXpltWhlaCNmfaCfWM&ll=12.873035405041499%2C121.77401750000001&z=6"
          width="600"
          height="500"
          style=" top: -50px; border: 0"
          loading="lazy"
        ></iframe>

        <!-- 
        <iframe
          width="600"
          height="450"
          style="border: 0"
          loading="lazy"
          allowfullscreen
          referrerpolicy="no-referrer-when-downgrade"
          src="https://www.google.com/maps/d/embed?mid=YOUR_CUSTOM_MAP_ID"
        >
        </iframe> -->
      </div>
      <div class="contact-container">
        <section id="contact">
          <h1 class="sectionTitle">Work with me!</h1>
          <form action="https://formspree.io/f/mqaqbzvl" method="POST">
            <div class="formGroup">
              <label for="name" hidden> Name </label>
              <input type="text" name="name" id="name" placeholder="Name" required />
            </div>
            <div class="formGroup">
              <label for="email" hidden> Email </label>
              <input type="text" name="email" id="email" placeholder="Email" required />
            </div>
            <div class="formGroup">
              <label for="message" hidden> Message </label>
              <textarea name="message" id="message" placeholder="Message" required></textarea>
            </div>
            <input class="hover btn" type="submit" value="Submit" />
          </form>
        </section>
      </div>
    </div>
  </div>
</template>

<style scoped>
.first-home {
  width: 100%;
  padding: 4rem 4rem 0 4rem;
  display: flex;
  flex-direction: row;
  background: #ffffff;
  align-items: center;
  justify-content: center;
}

.contact-container {
  background-color: #dc1b28;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 3vh;
  width: 50%;
  padding: 2rem;
}

.message-container {
  width: 50%;
  height: 100%;
  padding-top: 10rem;
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
</style>
