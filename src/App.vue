<script setup>
// import ConfettiCelebrationVue from './components/ConfettiCelebration.vue'
import ConfettiExplosion from "vue-confetti-explosion";
import { ref, onMounted } from "vue";
import axios from "axios";

const BASE_URL =
  import.meta.env.BASE_URL || "https://spotlight-backend.onrender.com";

// Define the spotlight state
const spotlight = ref("");

// Function to fetch data from the API
async function fetchData() {
  try {
    const response = await axios.get(
      "https://spotlight-backend.onrender.com/spotlight/employee"
    );
    if (!response?.data?.data) {
      spotlight.value = "No employee found";
      return;
    }

    spotlight.value = response.data.data;
    return;
  } catch (error) {
    console.error("Failed to fetch spotlight employee:", error);
    spotlight.value =
      "Sorry we are facing some issues. Please try again later...";
  }
}

// Call fetchData when the component mounts
onMounted(fetchData);
</script>

<template>
  <div class="main">
    <div class="confetti">
      <ConfettiExplosion :particleSize="10" />
    </div>

    <div class="main-content">
      <div class="section">
        <div>
          <!-- <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" /> -->
          <img
            src="https://www.proexelancers.com/images/proexelancers-logo.svg"
          />

          <div class="wrapper">
            <!-- <HelloWorld msg="You did it!" /> -->
          </div>
        </div>

        <div class="spotlight">
          Current person on spotlight - {&#123;
          <span class="employee-name">{{ spotlight }}</span> &#125;}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.timer {
  display: flex;
  justify-content: center;
}

.confetti {
  display: flex;
  justify-content: center;
}

.main {
  overflow: hidden;
}

.main-content {
  height: 93vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.employee-name {
  background: linear-gradient(309deg, rgb(76 221 72) 0%, rgb(253 255 255) 47%, rgb(255 143 0) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .spotlight {
    font-size: 50px;
  }
}

@media (min-width: 480px) {
  .spotlight {
    color: white;
    font-size: 30px;
  }
}
</style>
