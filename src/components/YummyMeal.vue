<template>
  <p>
    <strong>{{ name }}</strong>:
    <YummyMealPrice :price="price" />

    <button @click="addToCart">Add to cart</button>

  </p>
</template>

<script>
import { computed, provide } from 'vue';

import YummyMealPrice from './YummyMealPrice.vue';

export default {
  props: {
    name: String,
    price: Number,
  },
  components: {
    YummyMealPrice
  },

  setup(props, { emit }) {
    const name = props.name;
    const formatedName = computed(() => name.toUpperCase());
    provide('formatedName', formatedName);

    const addToCart = () => emit("addToCart", props.name);
    // const pricePretty3 = computed(() => {
    //   const formatedPrice = props.price.toFixed(2);
    //   console.log("in computed", "--formatedPrice--", formatedPrice);
    //   return `$${formatedPrice}`
    // });

    // const pricePretty = computed(() => `$${props.price.toFixed(2)}`);
    // const pricePrettySentence = computed(() =  > `${name} costs ${pricePretty.value}`);

    return { addToCart };

  },


}

</script>
