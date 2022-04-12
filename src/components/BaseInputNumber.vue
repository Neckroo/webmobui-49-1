<script setup>
  import { computed, ref } from "vue";
  import { roundToDecimalPlaces } from '../utils/math.js';

  const props = defineProps({
    modelValue: {
      type: [String, Number],
      required: true
    },
    symbol: {
      type: String,
      required: false,
      default: ''
    }
  })

  const emits = defineEmits([
    'update:modelValue'
  ]);

  const value = computed({
    get: () => roundToDecimalPlaces(props.modelValue, 2),
    set: val => {
      if (isNaN(val) || val === '') return;
      emits('update:modelValue', val)
    }
  })

</script>

<template>
  <input
    type="number"
    v-model="value"
  >
  <span>{{ symbol }}</span>
</template>

<style>

</style>
