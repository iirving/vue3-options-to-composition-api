<template>
  <p>
    <strong>{{ name }}</strong>:
    <YummyMealPrice :price="price" />

    <button @click="addToCart">Add to cart</button>

  </p>
</template>

<script setup>
import { computed, provide } from 'vue';
import YummyMealPrice from './YummyMealPrice.vue';

const props = defineProps({
  name: String,
  price: Number,
});
const name = props.name;

const formatedName = computed(() => name.toUpperCase());
provide('formatedName', formatedName);

const emit = defineEmits(['addToCart']);
const addToCart = () => emit("addToCart", props.name);
</script>
