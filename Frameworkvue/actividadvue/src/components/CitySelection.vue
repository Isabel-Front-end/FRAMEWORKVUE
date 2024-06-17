<!-- CitySelection.vue -->
<template>
    <div>
    <label for="city-selected">Selecciona una ciudad:</label>
    <select v-model="selectedCity" @change="selectCity">
    <option v-for="city in cities" :key="city.name" :value="city.name">{{ city.name }}</option>
    </select>
    </div>
    </template>
    
    <script>
    export default {
    data() {
    return {
    selectedCity: '',
    cities: [
    { name: 'New York' },
    { name: 'London' },
    { name: 'Paris' },
    { name: 'Sallanches' },
    { name: 'Liubliana' },
    { name: 'Albania' },
    { name: 'Chicago' },
    { name: 'MonteNegro' },
    { name: 'Venecia' }
    // Agrega más ciudades según sea necesario
    ]
    };
    },
    methods: {
    selectCity() {
    this.$emit('city-selected', this.selectedCity); // Cambiado de SelectedCity a selectedCity
    }
    }
    };
    </script>
    
    