<template>
  <div id="app">
    <tagList label="Tags" maxSelected="2" :tags="listFromApi" v-model="selectedTags"></tagList>
    output : {{selectedTags}}
  </div>
</template>

<script>
import axios from "axios";
import tagList from "./components/tagList";

export default {
  name: "App",
  components: {
    tagList
  },
  data() {
    return {
      listFromApi: null,
      selectedTags: null
    };
  },
  mounted() {
    axios
      .get(
        "https://api.projects.makesense.org/v1/taxonomies?limit=200&sort=-createdAt&type=legalForm"
      )
      .then(response => (this.listFromApi = response.data.data));
  }
};
</script>

<style>
#app {
  font-family: "Raleway", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #0c3944;
  max-width: 530px;
  width: 100%;
  margin: 60px auto;
}
</style>
