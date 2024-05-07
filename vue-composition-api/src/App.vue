<script>
import { computed, ref, reactive, toRef, toRefs, watch, watchEffect } from 'vue'

export default {
  setup () {
    const item = reactive({
      name: "Product 1",
      price: 10,
      quantity: 1,
    })

    const increment = () => item.quantity++

    const decrement = () => item.quantity--

    const swapProduct = () => {
      item.name = "Product A"
      item.price = 30
    }

    const total = computed(() => item.price * item.quantity)

    const { name, price, quantity } = toRefs(item)

    watch(() => item.quantity, () => {
      if(item.quantity === 5){
        item.quantity--
        alert("You cannot add more items")
      }
    }, { immediate: true } )

    watchEffect(() => {
      console.log('Price changed: ', item.price)
    })

    return {
      name,
      price,
      total,
      quantity,
      increment,
      decrement,
      swapProduct
    }
  }
}
</script>

<template>
  <div>
    <h1>{{ name }} : {{ price }}</h1>
    <button @click="swapProduct">Swap product</button>
    <button @click="price++">Change price</button>
    <h2>{{ quantity }}</h2>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <h3>Total: {{ total }}</h3>
  </div>
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
