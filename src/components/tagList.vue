<template>
  <div class="tag-list">taglist</div>
</template>

<script>
export default {
  name: "TagList",
  props: {
    label: String,
    maxSelected: Number,
    tags: Array
  },
  data() {
    return {
      selectedTags: []
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
</style>
