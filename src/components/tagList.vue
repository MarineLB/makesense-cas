<template>
  <div class="tag-list">
    <h3>{{ label }}</h3>
    <p>Selectionne {{ maxSelected }} tags dans la liste</p>
    <ul class="tag-list__tags tag-list__tags--selected">
      <li v-for="tag in tags" :key="tag._id" class="tag-list__tag">
        <button class="tag-list__tag-button tag-list__tag-button--selected">
          {{tag.name.fr}}
          <span class="tag-list__tag-icon tag-list__tag-icon--remove"></span>
        </button>
      </li>
    </ul>
    <ul class="tag-list__tags tag-list__tags--available">
      <li v-for="tag in tags" :key="tag._id" class="tag-list__tag">
        <button class="tag-list__tag-button">
          {{tag.name.fr}}
          <span class="tag-list__tag-icon tag-list__tag-icon--add"></span>
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
<style lang="scss" scoped>
.tag-list__tags {
  list-style-type: none;
  display: flex;
  flex-wrap: wrap;
  padding: 0;

  &--available {
    border: 2px dashed #e8e8e8;
    padding: 15px;
    border-radius: 5px;
  }
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
  padding: 10px 15px;
  border-radius: 50px;
  cursor: pointer;
  display: flex;
  align-items: center;
  font-family: inherit;

  &:hover {
    background: #979797;
    color: white;
  }

  &--selected {
    background: #fabe3c;
    border: 2px solid #fabe3c;
    color: white;
    font-weight: 800;
    &:hover {
      background: white;
      color: #fabe3c;
    }
  }
}
.tag-list__tag-icon {
  &:before {
    margin-left: 5px;
    font-size: 1rem;
  }
  &--add:before {
    content: "+";
  }
  &--remove:before {
    content: "-";
  }
}
</style>
