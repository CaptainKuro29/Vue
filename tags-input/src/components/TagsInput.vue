<template>
  <div>
    <div class="tags-input-wrapper">
      <span class="tag-item" v-for="(tag, index) in tags" :key="index">
        <b>
          {{ tag }}
        </b>
        <a class="removeTag" @click.prevent="removeTag(index)" href="#">
          &times;
        </a>
      </span>
      <input
        type="text"
        class="tag-input"
        v-model.trim="newTag"
        @keydown.enter="addNewTag"
        placeholder="Add a new tag"
        @keydown.tab.prevent="addNewTag"
        :class="{ 'tag-exists': isTagExists }"
      />
      <a @click="addTag(newTag)" href="#">Add</a>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      tags: [...this.selectedTags],
      newTag: ""
    }
  },
  props: {
    selectedTags: {
      type: Array,
      required: true,
      default: () => []
    }
  },
  watch: {
    newTag(newVal) {
      if (newVal.indexOf(",") > -1) {
        this.newTag = this.newTag.slice(0, -1);
        this.addNewTag();
      }
    },
  },
  computed: {
    isTagExists() {
      return this.tags.includes(this.newTag);
    },
  },
  emits: ["change"],
  methods: {
    addNewTag() {
      if (this.newTag && !this.isTagExists) {
        this.tags.push(this.newTag);
        this.newTag = "";
        this.$emit('change', this.tags);
      }
      if (this.tags.includes(this.newTag)) {
        alert("This task already exists.");
        this.newTag = "";
      }
    },
    removeTag(index) {
      this.tags.splice(index, 1);
      this.$emit('change', this.tags);
    },
    addTag(tag) {
      this.newTag = tag;
      if (this.newTag && !this.isTagExists) {
        this.tags.push(this.newTag);
        this.newTag = "";
        this.$emit('change', this.tags);
      }
      if (this.tags.includes(this.newTag)) {
        alert("This task already exists.");
        this.newTag = "";
      }
    },
  },
};
</script>
<style scoped>
h2 {
  color:#495057;
}
.tag-input.tag-exists {
  color: red;
  text-decoration: line-through;
}

.tags-input-wrapper {
  background: #fff;
  padding: 0.5em;
  border: 1px solid #dbdbdb;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  min-height: 36px;
  box-sizing: border-box;
}

.tag-item {
  color: #212529;
  background-color: #eee;
  margin-right: 0.3em;
  padding: 0.25em 0.4em;
  /* font-size: 75%; */
  line-height: 1;
  text-align: center;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  padding-right: 1.25em;
  padding-left: 0.6em;
}

.tag-input {
  color: #495057;
  flex: 1;
  background: transparent;
  border: none;
}

.tag-input:focus {
  outline: none;
}

a.remove-tag {
  text-decoration: none;
}
</style>
