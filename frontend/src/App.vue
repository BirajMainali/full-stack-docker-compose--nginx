<script setup lang="ts">
import { onMounted, ref } from 'vue';
import axios from "axios";

const weatherforecast = ref<[{}]>([{}])

const isLoading = ref(true);

const getWeatherForecast = async () => {
  const baseUrl = import.meta.env.VITE_API_ENDPOINT;
  const data = await axios.get(`${baseUrl}/WeatherForecast`, {
    headers: {
      'Content-Type': 'application/json',
    },
  });
  weatherforecast.value = data.data;
  console.log(weatherforecast.value);
}

onMounted(async () => {
  await getWeatherForecast();
  isLoading.value = false;
})

</script>


<template>
  <div v-if="!isLoading">
    <h2>WeatherForecast</h2>
    <ul>
      <li v-for="(forecast, index) in weatherforecast" :key="index">
        {{ forecast }}
      </li>
    </ul>
  </div>
  <div v-else>
    Loading...
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
