<template>
  <div class="home">
    <div class="first-home">
      <div class="left-container">
        <h1>Contact Us</h1>
        <h2>Reach and Contact us for a future that’s brighter than ever</h2>
        <div class="callus-container">
        <h1>Call Us</h1>
        <div class="inner-icons"> 
          <img src="/src/components/icons/Frame.svg" alt=""><h1>#000-000-000</h1>
        </div>
       </div>
        <iframe
          src="https://www.google.com/maps/d/u/0/embed?mid=1NBYf_O7PJTmSs1sjaknUWhbYFhgZC0w&ehbc=2E312F"
          width="400"
          height="400"
          style=" top: -50px; border: 0"
          loading="lazy"
        ></iframe>
       

       <div class="visitus-container">
        <div class="inner-icons">

        </div>
       </div>
      </div>
      <div class="right-container">
        <section id="contact">
          <!-- <h1 class="sectionTitle">Work with me!</h1> -->
          <form action="https://formspree.io/f/mqaqbzvl" method="POST">
            <div class="formGroup">
              <label for="name" style="color: white;"> Name </label> <br>
              <input type="text" name="name" id="name" style="width: 45vh; border-radius: 2vh; border-style: none;" required />
            </div>
            <div class="formGroup">
              <label for="email" style="color: white;"> Email </label> <br>
              <input type="text" name="email" id="email"  style="width: 45vh; border-radius: 2vh; border-style: none;" required />
            </div>
            <div class="formGroup">
              <label for="message" style="color: white;"> Message </label> <br>
              <textarea name="message" id="message" style="width: 45vh; min-height: 30vh; max-width: 45vh; border-radius: 2vh; border-style: none;" required></textarea>
            </div>
            <input class="hover btn" type="submit" value="Submit" style="padding: 1vh; border-radius: 1vh; border-style: none; color: #dc1b28; background-color: #FFFFFF;" />
          </form>
        </section>
      </div>
    </div>
  </div>
</template>

<style scoped>
.inner-icons{
  display: flex;
  flex-direction: row;
  align-items: center;
  /* justify-content: center; */
  margin-top: 1rem;
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

.right-container {
  background-color: #dc1b28;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 3vh;
  width: 50%;
  padding: 2rem;
}

.left-container {
  width: 50%;
  height: 100%;
  /* padding-top: 10rem; */
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
