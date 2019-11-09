<template>
  <div class="tag-list">
    <h3>{{ label }}</h3>
    <p>Selectionne {{ maxSelected }} tags dans la liste</p>
    <ul class="tag-list__available-tags">
      <li v-for="tag in tags" :key="tag._id" class="tag-list__tag">
        <button class="tag-list__tag-button">
          {{tag.name.fr}}
          <span class="tag-list__tag-icon"></span>
        </button>
      </li>
    </ul>
  </div>
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
<style  scoped>
.tag-list__available-tags {
  list-style-type: none;
  border: 2px dashed #e8e8e8;
  padding: 15px;
  display: flex;
  flex-wrap: wrap;
  border-radius: 5px;
}
.tag-list__tag {
  margin: 5px;
}
.tag-list__tag-button {
  outline: none;
  background: none;
  border: 2px solid #979797;
  color: #979797;
  font-weight: 600;
  font-size: 1rem;
  padding: 15px 7.5px;
  border-radius: 50px;
  cursor: pointer;
  display: flex;
  align-items: center;
  font-family: inherit;
}
.tag-list__tag-button:hover {
  background: #979797;
  color: white;
}
.tag-list__tag-icon:before {
  content: "+";
  margin-left: 5px;
  font-size: 1rem;
}
</style>
