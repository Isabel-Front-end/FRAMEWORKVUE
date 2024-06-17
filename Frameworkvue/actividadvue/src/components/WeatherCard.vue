<!-- WeatherCard.vue -->
<template>
    <div class="weather-card">
    <h3>{{ weather.time }}</h3>
    <p>{{ weather.temperature }} °C</p>
    <p>{{ weather.description }}</p> <!-- Agrega esta línea para mostrar la descripción del clima -->
    </div>
    </template>
    
    <script>
    export default {
    props: ['weather'],
    methods: {
    kelvinToCelsius(temp) {
    return (temp - 273.15).toFixed(1);
    }
    }
    };
    </script>
    
    <style scoped>
    .weather-card {
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 10px;
    margin: 10px;
    }
    </style>
    

    