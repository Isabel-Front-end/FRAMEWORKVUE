<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import CitySelection from './components/CitySelection.vue';
import WeatherCard from './components/WeatherCard.vue';
export default {
components: {
CitySelection,
WeatherCard
},
data() {
return {
weatherData: null
};
},
methods: {
async getWeatherData(city) {
try {
const response = await axios.get(`https://api.tomorrow.io/v4/timelines?location=${city}&fields=temperature&timesteps=current&apikey=1zlTVsyoTqjrxnvBiqTULXjygeulwl30`);
console.log('Response:', response);
this.weatherData = response.data.data.timelines[0].intervals.map(interval => ({
time: interval.startTime,
temperature: this.kelvinToCelsius(interval.values.temperature),
description: interval.values.temperature.description // Ajusta según la estructura de tu respuesta API
}));
} catch (error) {
console.error('Error fetching weather data:', error);
}
},
kelvinToCelsius(temp) {
return (temp - 273.15).toFixed(1);
}
}
};


</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
    <div>
<CitySelection @city-selected="getWeatherData" />
<div v-if="weatherData" class="weather-cards">
<WeatherCard v-for="(weather, index) in weatherData" :key="index" :weather="weather" />
</div>
</div>

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
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

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
