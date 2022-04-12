<script setup>

  import { ref, computed } from '@vue/reactivity';
  import BaseInputNumber from './BaseInputNumber.vue';

  const props = defineProps({
    title: {
      type: String,
      required: true
    },
    // each unit must be an object int the units array like this one:
    // [
    //   {label: 'Kelvin', symbol: 'K', get: val => val, set: val => val}
    //   {label: 'Celsius', symbol: '°C', get: val => val + 237.15, set: val => val - 273.15}
    // ]
    units: {
      type: Array,
      required: true
    },
    decimalPlaces: {
      type: Number,
      required: false,
      default: 2
    },
    decimalPlacesEditable: {
      type: Boolean,
      required: false,
      default: false
    }
  });

  const baseUnit = ref(0);

  const computedValues = [];
  for (const unit of props.units) {
    computedValues.push(computed({
      get: () => unit.get(baseUnit.value),
      set: val => baseUnit.value = unit.set(val)
    }));
  }

  const decimalPlaces = ref(props.decimalPlaces);

</script>

<template>

  <h1>{{ title }}</h1>

  <template v-if="decimalPlacesEditable">
    <label>Round to decimal places : </label>
    <base-input-number
      v-model="decimalPlaces"
      :decimal-places="0"
      min="0"
      max="12"
    />
  </template>

  <template v-for="(unit, index) in units">
    <label>{{unit.label}}</label>
    <base-input-number
      v-model="computedValues[index].value"
      :decimal-places="decimalPlaces"
      :symbol="unit.symbol"
    />
  </template>

</template>

<style scoped>
  label {
    display: block;
    margin: 1rem 0 0.5rem 0;
    font-size: 1.2rem;
  }
</style>
