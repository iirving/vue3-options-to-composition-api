<template>
  <span>
    {{ pricePretty }}
  </span>
</template>

<script>
import { computed, inject } from 'vue';
export default {
  props: {
    price: Number,
  },

  setup(props) {
    const currencySymbol = inject('currencySymbol');
    const pricePretty = computed(() => {
      const formatedPrice = props.price.toFixed(2);
      // console.log("in computed", "--formatedPrice--", formatedPrice);
      return `${currencySymbol}${formatedPrice}`
    });

    // const pricePretty = computed(() => `$${props.price.toFixed(2)}`);

    return { pricePretty };

  }
}

</script>
