<script setup>
  const props = defineProps({
    temperature: {
      type: Number,
      required: false,
      default: 20
    }
  })

  console.log(props.temperature)

</script>

<template>
  <button :class="`temp_${temperature}`">
    <slot>Test</slot>
  </button>
</template>

<style scoped>
  .alert {
    color: red;
  }
</style>