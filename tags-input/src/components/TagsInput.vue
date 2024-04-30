<template>
  <div>
    <h2>My List :</h2>
    <div v-for="(tag, index) in tags" :key="tag">
      <b>
        {{ tag }}
      </b>
      <button @click.prevent="removeTag(index)">&times;</button>
    </div>
    <hr />
    <h2>Add to the list :</h2>
    <p>{{ newTag }}</p>
    <input
      type="text"
      v-model.trim="newTag"
      @keydown.tab.prevent="addNewTag"
      @keydown.enter="addNewTag"
    />
  </div>
</template>
<script>
export default {
  data: () => ({
    tags: ["vue", "react", "angular"],
    newTag: "preact",
  }),
  methods: {
    addNewTag() {
      if (this.newTag) {
        this.tags.push(this.newTag);
        this.newTag = "";
      }
    },
    removeTag(index) {
        this.tags.splice(index, 1)
    }
  },
};
</script>
<style scoped>
ul {
  list-style: none;
  padding-left: 0px;
}

p {
  text-decoration: underline;
  color: #e25822;
}

h2 {
  color: #29ab87;
}


b {
    color: #00BFFF;
}

input {
    border-radius: 5px;
    border: 1px solid lightblue;
    padding: 10px;
}

button {
    margin: 5px;
}
</style>
