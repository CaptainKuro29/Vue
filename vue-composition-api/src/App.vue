<script>
import { computed, ref, reactive, toRef, toRefs } from 'vue'

export default {
  setup () {
    const message = ref("Hello")
    const quantity = ref(1)
    const item = reactive({
      name: "Product 1",
      price: 10
    })

    const increment = () => quantity.value++

    const decrement = () => quantity.value--

    const swapProduct = () => {
      item.name = "Product A"
      item.price = 30
    }

    const { name, price } = toRefs(item)

    return {
      message,
      quantity,
      increment,
      decrement,
      name,
      price,
      swapProduct
    }
  }
}
</script>

<template>
  <div>
    <h1>{{ name }} : {{ price }}</h1>
    <button @click="swapProduct">Swap product</button>
    <h2>{{ quantity }}</h2>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
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
