<script>
import TagsInput from "./components/TagsInput.vue";

export default {
  components: {
    // TagsInput
  }
}
</script>

<template>
  <div>
    <h1>Todo List</h1>
    <tags-input></tags-input>
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

h1 {
  color: #03C03C;
}
</style>
