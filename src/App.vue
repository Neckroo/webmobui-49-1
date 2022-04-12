<script setup>
  import TheNav from './components/TheNav.vue';
  import BaseInputNumber from './components/BaseInputNumber.vue';
  import { page } from './state.js';
  import { ref } from 'vue';

  const celsius = ref(12);
  const kelvin = ref(12);
</script>

<template>
  <the-nav></the-nav>
  <base-input-number
    symbol="°C"
    :modelValue="celsius"
    @update:modelValue="celsius = $event"
  />
  <base-input-number
    symbol="K"
    v-model="kelvin"
  />
  <div>{{ celsius }}</div>
  <div>{{ kelvin }}</div>
</template>

<style>

</style>
