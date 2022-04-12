<script setup>
  import AppConverter from './components/AppConverter.vue';
  import TheNav from './components/TheNav.vue';
  import { store } from './store.js';

  const temperatureUnits = [
    {
      label: 'Kelvin', symbol: 'K',
      get: val => val,
      set: val => val
    }, {
      label: 'Celsius', symbol: '°C',
      get: val => val + 273.15,
      set: val => val - 273.15
    }, {
      label: 'Fahrenheit', symbol: '°F',
      get: val => val * 1.8 - 459.67,
      set: val => (val + 459.67) / 1.8
    }
  ];

  const dataStorageUnits = [
    {
      label: 'Byte', symbol: 'B',
      get: val => val,
      set: val => val
    }, {
      label: 'Megabyte', symbol: 'MB',
      get: val => val / 1e+6,
      set: val => val * 1e+6
    }, {
      label: 'Gigabyte', symbol: 'GB',
      get: val => val / 1e+9,
      set: val => val * 1e+9
    }, {
      label: 'Terabyte', symbol: 'TB',
      get: val => val / 1e+12,
      set: val => val * 1e+12
    }
  ];
</script>

<template>

  <the-nav></the-nav>

  <template v-if="store.page == 'home'">
    <h1>Welcome to the converter app</h1>
  </template>

  <app-converter
    v-if="store.page == 'temperature'"
    :units="temperatureUnits"
    :decimalPlacesEditable="true"
    title="Temperature"
  />

  <app-converter
    v-if="store.page == 'data-storage'"
    :units="dataStorageUnits"
    :decimal-places="12"
    title="Data storage"
  />

</template>

<style>
  * {
    box-sizing: border-box;
  }
</style>
