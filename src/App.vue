<template>
  <div id="app"></div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  components: {},
  data() {
    return {
      apiURL: "https://api.themoviedb.org/3/search/movie",
      apiKey: "5ec423d0e09c1c7875d6ca5bd8343d0a",
    };
  },
  mounted() {
    const par = {
      query: "verde",
      api_key: this.apiKey,
    };

    axios
      .get(this.apiURL, { par })
      .then((risp) => console.log(risp))
      .catch((err) => console.log(err));
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
