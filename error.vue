<template>
  <div>
    <Navbar />
    <div class="video_v">
      <video autoplay="autoplay" loop="loop" muted="muted">
        <source src="./assets/video/404.webm" />
      </video>
      <div class="banner">
        <NuxtLink to="/" class="butn butn__new" @click="handleClearError"
          ><span>Go Back Home</span></NuxtLink
        >
      </div>
    </div>
    <!-- <p class="mt-7 text-7xl font-bold">{{ error.statusCode }}</p> -->
    <!-- <p class="mt=7 text-6xl">Ooops.</p> -->
    <!-- <p class="mt-7">{{ error.message }}</p> -->

    <!-- <button class="btn my-7" @click="handleClearError">Go Home...</button> -->
    <Footer />
  </div>
</template>

<script setup>
defineProps(["error"]);

const handleClearError = () => clearError({ redirect: "/" });
</script>

<style scoped>
.video_v {
  display: flex;
  flex-direction: column;
  gap: 40px;
  align-items: center;
  justify-content: center;
  margin-top: 200px;
  margin-bottom: 50px;
}

a,
a:hover {
  text-decoration: none;
}

.butn:link,
.butn:visited {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-size: 17px;
  /* text-transform: uppercase; */
  text-decoration: none;
  background-color: #5e16bd;
  background-image: linear-gradient(90deg, #e3b269, #e3b269, #9b7439);
  padding: 16px, 32px, 16px, 32px;
  height: 50px;
  width: 170px;
  border-radius: 8px;

  margin-right: 13px;
  font-weight: 600;
  border: none;
  color: #030303;
  position: relative;
  overflow: hidden;
  transition: all 0.3s ease-in-out;
}
.butn::before {
  background: #fff;
  content: "";
  height: 155px;
  opacity: 0;
  position: absolute;
  top: -50px;
  transform: rotate(35deg);
  width: 15px;
  transition: all 3000ms cubic-bezier(0.19, 1, 0.22, 1);
}
.butn::after {
  background: #fff;
  content: "";
  height: 15rem;
  opacity: 0;
  position: absolute;
  top: -50px;
  transform: rotate(35deg);
  transition: all 3000ms cubic-bezier(0.19, 1, 0.22, 1);
  width: 4rem;
}
.butn__new::before {
  left: -50%;
}

.butn__new::after {
  left: -100%;
}

.butn:hover,
.butn:active {
  transform: translateY(-3px);
  color: #000;
  box-shadow: 0 10px 20px 0 rgba(0, 0, 0, 0.3);
}

.butn__new:hover::before {
  left: 120%;
  opacity: 0.5s;
}

.butn__new:hover::after {
  left: 200%;
  opacity: 0.6;
}
.butn span {
  z-index: 20;
}
</style>
