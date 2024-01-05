<template>
  <span>
    {{ pricePretty }}
  </span>
</template>

<script>
import { computed } from 'vue';
export default {
  props: {
    price: Number,
    currencySymbol: String

  },

  setup(props) {
    const pricePretty = computed(() => {
      const formatedPrice = props.price.toFixed(2);
      // console.log("in computed", "--formatedPrice--", formatedPrice);
      return `${props.currencySymbol}${formatedPrice}`
    });

    // const pricePretty = computed(() => `$${props.price.toFixed(2)}`);

    return { pricePretty };

  }
}

</script>
