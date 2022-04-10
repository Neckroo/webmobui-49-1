<script setup>
  import { ref, computed, watchEffect } from 'vue';

  const tempSI = ref(0); // kelvin

  const celsius = computed({
    get: () => tempSI.value - 273.15,
    set: val => tempSI.value = val + 273.15
  });

  const kelvin = computed(() => tempSI.value);

  const fahrenheit = computed(() => (tempSI.value - 273.15) * 1.8 + 32);

  watchEffect(() => {
    console.log('°C', celsius.value);
    console.log('K', kelvin.value);
    console.log('°F', fahrenheit.value);
  });

  setTimeout(() => {
    tempSI.value = 300;
  }, 1000)


  setTimeout(() => {
    celsius.value = 40;
  }, 5000)
</script>

<template>
  <h1>Temperatures converter</h1>
  <div>Celsius: </div>
  <div>{{ celsius }}</div>
  <div>Kelvin: </div>
  <div>{{ kelvin }}</div>
  <div>{{ fahrenheit }}</div>
</template>

<style>

</style>
