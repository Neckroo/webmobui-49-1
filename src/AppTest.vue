<script setup>
  import { ref, computed, watchEffect } from 'vue';
 import BaseButton from './components/BaseButton.vue';
 import TheNav from './components/TheNav.vue';

  const tempSi = ref(0); // kelvin

  const kelvin = computed({
    get: () => tempSi.value,
    set: val => tempSi.value = val
  });

  const celsius =  computed({
    get: () => tempSi.value - 273.15,
    set: val => tempSi.value = val + 273.15
  });

  const fahrenheit =  computed({
    get: () => tempSi.value * 1.8 - 459.67,
    set: val => tempSi.value = (val + 459.67) / 1.8
  });

  watchEffect(() => {
    console.log('°C', celsius.value);
    console.log('K', kelvin.value);
    console.log('°F', fahrenheit.value);
  });

  setTimeout(() => {
    tempSi.value = 300;
  }, 1000)


  setTimeout(() => {
    celsius.value = 0;
  }, 5000)

  const msgTemp = computed(() => celsius.value < 20 ? 'froid' : 'chaud')

  function showCelsius(t) {
    return `${t} [°C]`;
  }

  const pi = Math.PI;

  const page = ref('home');
</script>

<template>

  <the-nav @page-change="page = $event"></the-nav>

  <div v-show="page == 'temp'">
    <h1>Temperatures converter</h1>
    <div>Celsius: </div>
    <div :class="msgTemp"> {{ showCelsius(celsius) }}</div>
    <div>{{ msgTemp }}</div>
    <div>Kelvin: </div>
    <div>{{ kelvin }}</div>
    <div>{{ fahrenheit }}</div>
    <div>{{ pi }}</div>
    <base-button class="alert" :temperature="celsius">
      <b>Delete</b>
    </base-button>
    <base-button></base-button>
    <base-button>Btn 3</base-button>
    <div v-if="celsius < 10 ">Attention c'est trop froid</div>
  </div>

</template>

<style>

  .froid {
    color: blue;
  }
  .chaud {
    color: red;
  }
</style>
