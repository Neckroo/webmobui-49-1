<script setup>
  import { page } from '../state.js';

  window.addEventListener('hashchange', () => {
    page.value = window.location.hash;
  })

  page.value = window.location.hash || '#home';
</script>

<template>
  <nav>
    <ul>
      <li>
          <a href="#home">Home</a>
      </li>
      <li>
          <a href="#temprature">Temperature</a>
      </li>
    </ul>
  </nav>
</template>

<style>

</style>
