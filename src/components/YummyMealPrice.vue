<template>
  <span>
    {{ pricePretty }}
    <!-- {{ formatedName }} -->
  </span>
</template>

<script>
import { computed, inject, ref } from 'vue';
export default {
  props: {
    price: Number,
  },

  setup(props) {
    const currencySymbol = inject('currencySymbol');
    const formatedName = inject('formatedName');
    const pricePretty = computed(() => {
      const formatedPrice = props.price.toFixed(2);
      console.log("in computed", "--formatedPrice--", formatedPrice);
      return `${currencySymbol.value}${formatedPrice}`
    });

    // const pricePretty = computed(() => `$${props.price.toFixed(2)}`);

    return { pricePretty, formatedName };

  }
}

</script>
