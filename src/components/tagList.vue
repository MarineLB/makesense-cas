<template>
  <div class="tag-list">
    <h3>{{ label }}</h3>
    <p>{{message}}</p>
    <select name="lang" v-model="lang">
      <option value="fr">Francais</option>
      <option value="en">English</option>
      <option value="en">Español</option>
    </select>
    <ul class="tag-list__tags tag-list__tags--selected">
      <li v-for="tagId in selectedTags" :key="tagId" class="tag-list__tag">
        <button
          @click="removeFromSelected(tagId)"
          class="tag-list__tag-button tag-list__tag-button--selected"
        >
          {{getTagName(tagId)}}
          <span class="tag-list__tag-icon tag-list__tag-icon--remove"></span>
        </button>
      </li>
    </ul>
    <ul class="tag-list__tags tag-list__tags--available">
      <li v-for="tag in availableTags" :key="tag._id" class="tag-list__tag">
        <button @click="addToSelected(tag._id)" class="tag-list__tag-button">
          {{tag.name[lang]}}
          <span class="tag-list__tag-icon tag-list__tag-icon--add"></span>
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "tagList",
  props: {
    label: String,
    maxSelected: String,
    tags: Array // filter by not selected tags
  },
  data() {
    return {
      selectedTags: [],
      lang: "fr"
    };
  },
  computed: {
    availableTags() {
      // filter tags that are not selected
      return this.tags
        ? this.tags.filter(tag => {
            return !this.selectedTags.includes(tag._id);
          })
        : [];
    },
    countSelected() {
      return this.selectedTags.length;
    },
    message() {
      if (this.countSelected === 0) {
        return `Selectionne ${
          this.maxSelected
        } ${this.getTagPlural()} dans la liste`;
      } else if (this.countSelected < this.maxSelected) {
        return `Selectionne encore ${this.maxSelected -
          this.countSelected} ${this.getTagPlural()} dans la liste`;
      } else {
        return `Vous devez enlever 1 tag sélectionné pour en choisir un autre`;
      }
    }
  },
  methods: {
    addToSelected(id) {
      if (this.countSelected < this.maxSelected) {
        this.selectedTags.push(id);
      }
      this.emitValue();
    },
    removeFromSelected(id) {
      this.selectedTags.splice(this.selectedTags.indexOf(id), 1);
      this.emitValue();
    },
    getTagPlural() {
      return this.maxSelected - this.countSelected === 1 ? "tag" : "tags";
    },
    getTagName(id) {
      return this.tags.find(tag => {
        return tag._id == id;
      }).name[this.lang];
    },
    emitValue() {
      this.$emit("input", this.selectedTags);
    }
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
    content: "x";
  }
}
</style>
