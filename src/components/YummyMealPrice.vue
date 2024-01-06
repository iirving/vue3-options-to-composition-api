<template>
  <span>
    {{ pricePretty }}
    <!-- {{ formatedName }} -->
  </span>
</template>

<script setup>
import { computed, inject, ref } from 'vue';

const props = defineProps({
  price: Number,
});
const currencySymbol = inject('currencySymbol');
const formatedName = inject('formatedName');
const pricePretty2 = computed(() => {
  const formatedPrice = props.price.toFixed(2);
  console.log("in computed", "--formatedPrice--", formatedPrice);
  return `${currencySymbol.value}${formatedPrice}`
});
const pricePretty = computed(() => `${currencySymbol.value}${props.price.toFixed(2)}`);



</script>
