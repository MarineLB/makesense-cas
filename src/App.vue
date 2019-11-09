<template>
  <div id="app">
    {{tags}}
    <tagList></tagList>
  </div>
</template>

<script>
import axios from 'axios'
import tagList from "./components/tagList";

export default {
  name: "App",
  components: {
    tagList
  },
  data() {
    return {
      tags: null
    }
  },
  mounted () {
    axios
      .get('https://api.projects.makesense.org/v1/taxonomies?limit=200&sort=-createdAt&type=legalForm')
      .then(response => (this.tags = response))
  }
};
</script>

<style>
#app {
  font-family: "Raleway", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #0C3944;
  margin-top: 60px;
}
</style>
