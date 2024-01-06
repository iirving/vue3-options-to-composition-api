<script >
import YummyMeal from './components/YummyMeal.vue';
import { ref, reactive, watch, watchEffect, provide } from 'vue';

export default {
  components: {
    YummyMeal
  },
  setup() {

    provide('currencySymbol', '$');

    const name = ref('the place to be');
    console.log("in set up", "--name-value--", name.value);

    // const badName = reactive('another the place to be'); // reactive can't be used on primitive types

    const meal = ref({
      name: 'Pizza',
      price: 10
    });
    console.log("in set up", "--meal-name-value--", meal.value.name);

    const meal2 = reactive({
      name: 'Burger',
      price: 8
    });

    console.log("in set up", "--meal2-name--", meal2.name);
    const meals = ref([
      {
        name: 'Pizza',
        price: 10
      },
      {
        name: 'Burger',
        price: 8
      },
      {
        name: 'Pasta',
        price: 12
      },
      {
        name: 'Salad',
        price: 6
      },
    ])
    const cart = ref([]);

    const placeOrder = () => {
      console.log('Order placed!');
      alert('Order has been placed!');
    }

    const addItemToCart = (item) => cart.value.push(item);

    const HideCart = watch(() => [...cart.value], (newCart, oldCart) => {
      // console.log("in watch ", "--newName--", newCart, "--oldName--", oldCart);
      const puralItem = newCart.length > 1 ? 'items' : 'item';
      alert(`${newCart.length} ${puralItem} in cart:\n\n${newCart.join('\n')}`);
    });

    // watch([name, () => [...cart.value]], (newName, oldName) => {
    //   console.log("in watch ", "--newName--", newName, "--oldName--", oldName);
    // });

    watchEffect(() => {
      console.log("in watchEffect ", "--name--", name);
      console.log("in watchEffect ", "--cart--", cart);
      console.log("in watchEffect ", "--cart.value--", cart.value);
      // console.log("in watchEffect ", "--cart.value.length--", cart.value.length);
      if (cart.value.length < 0) {
        console.log("in watchEffect ", "--cart.value.length--", cart.value.length);
      }
      console.log("in watchEffect ", "--meals--", meals);

    });

    // const removeWatcher = watch([() => [...cart.value]], (newValue, oldValue) =>
    //   alert(newValue.join("\n")));


    return { name, placeOrder, addItemToCart, meal, meal2, meals, HideCart };

  }
};

</script>

<template>
  <h1>{{ name }}</h1>
  <label for="currencySymbol">Currency</label>
  <select id="currencySymbol" v-model="currencySymbol"></select>
  <option value="$">US Dollars ($)</option>
  <option value="£">British Pounds (£)</option>
  <option value="€">Euros (€)</option>
  <option value="$">Canadian Dollar ($)</option>
  <option value="¥">Japanese Yen (¥)</option>
  <option value="₹">Indian Rupees (₹)</option>
  <option value="₽">Russian Rubles (₽)</option>
  <option value="₩">South Korean Won (₩)</option>
  <option value="₿">Bitcoin (₿)</option>
  <option value="฿">Thai Baht (฿)</option>
  <option value="₺">Turkish Lira (₺)</option>
  <option value="₴">Ukrainian Hryvnia (₴)</option>
  <option value="₮">Mongolian Tögrög (₮)</option>
  <option value="₦">Nigerian Naira (₦)</option>
  <option value="₱">Philippine Peso (₱)</option>
  <option value="₡">Costa Rican Colón (₡)</option>
  <input v-model="name" />
  <button @click="placeOrder">Place Order</button>
  <button @click="HideCart">Hide Cart Alerts</button>
  <br />
  <span>
    <YummyMeal v-for="meal in meals" :name="meal.name" :price="meal.price" @addToCart="addItemToCart" />
  </span>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
