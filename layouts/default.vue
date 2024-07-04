<template>
  <div>
    <!-- Overlay Section -->
    <div v-if="!isLoaded" class="overlay">
      <div class="overlayDoor"></div>
      <div class="overlayContent">
        <div class="loader">
          <div class="inner"></div>
        </div>
        <!--        <div class="skip" @click="skipLoading">SKIP</div>-->
      </div>
    </div>

    <!-- Content Section (not needed, keeping for context) -->
    <!-- <div class="header">
      <div class="darken">
        <h1>
          The page has fully loaded!<br /><span>Or you skipped...</span>
        </h1>
      </div>
    </div>
    <div class="contentOther">
      <h1>This waits for EVERYTHING to load on the page.</h1>
      <h1>Random Video</h1>
      <iframe
        class="video"
        src="https://www.youtube.com/embed/mZY1yyrlJWU"
        frameborder="0"
        allowfullscreen
      ></iframe>
    </div> -->

    <div>
      <Navbar />
      <slot />
      <Footer />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const isLoaded = ref(false);

const skipLoading = () => {
  isLoaded.value = true;
  document.body.classList.add("loaded");
};

onMounted(() => {
  // Simulate page load completion
  window.addEventListener("load", () => {
    isLoaded.value = true;
    document.body.classList.add("loaded");
    setTimeout(() => {
      if (document.querySelector(".overlay")) {
        document.querySelector(".overlay").style.display = "none";
      }
    }, 2000);
  });

  // Automatically remove the overlay after 1 minute
  setTimeout(() => {
    isLoaded.value = true;
    document.body.classList.add("loaded");
  }, 2000);
});
</script>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css?family=Nunito:400,600,700|Roboto:300,400,500,700");

body {
  margin: 0;
  padding: 0;
  overflow: hidden;
  &.loaded {
    overflow-y: auto;
  }
}

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 100000000;

  .overlayDoor {
    &:before,
    &:after {
      content: "";
      position: absolute;
      width: 50%;
      height: 100%;
      background: #111;
      transition: 0.5s cubic-bezier(0.77, 0, 0.18, 1);
      transition-delay: 0.8s;
    }

    &:before {
      left: 0;
    }

    &:after {
      right: 0;
    }
  }

  &.loaded {
    .overlayDoor {
      &:before {
        left: -50%;
      }

      &:after {
        right: -50%;
      }
    }

    .overlayContent {
      opacity: 0;
      margin-top: -15px;
    }
  }

  .overlayContent {
    position: relative;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    transition: 0.5s cubic-bezier(0.77, 0, 0.18, 1);

    .skip {
      display: block;
      width: 130px;
      text-align: center;
      margin: 50px auto 0;
      cursor: pointer;
      color: #1a8377;
      font-family: "Nunito";
      font-weight: 700;
      padding: 12px 0;
      border: 2px solid #1a8377;
      border-radius: 3px;
      transition: 0.2s ease;

      &:hover {
        background: #ddd;
        color: #444;
        border-color: #1a8377;
      }
    }
  }
}

.loader {
  width: 128px;
  height: 128px;
  border: 7px solid #e3b269;
  border-bottom: 3px solid transparent;
  border-radius: 50%;
  position: relative;
  animation: spin 1s linear infinite;
  display: flex;
  justify-content: center;
  align-items: center;

  .inner {
    width: 64px;
    height: 64px;
    border: 3px solid transparent;
    border-top: 7px solid #e3b269;
    border-radius: 50%;
    animation: spinInner 1s linear infinite;
  }
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

@keyframes spinInner {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(-720deg);
  }
}
</style>

<style lang="scss" scoped></style>
