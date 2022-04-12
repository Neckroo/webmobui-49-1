<script setup>
  import { ref } from "@vue/reactivity";
  import { watchEffect } from "@vue/runtime-core";

  const emits = defineEmits([
    "page-change"
  ]);

  const page = ref('home');
  watchEffect(() => {
    emits("page-change", page.value);
  });

</script>

<template>
  <nav>
    <ul>
      <li>
        <a href="#temp" @click="page='temp'">Temp</a>
      </li>
      <li>
          <a href="#byte"  @click="page='byte'">Byte</a>
      </li>
    </ul>
  </nav>
</template>

<style scoped>

</style>
