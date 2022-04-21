<template>
  <div id="app">
    <div class="input-group">
      <input
        class="form-control"
        type="text"
        placeholder="Cerca"
        v-model="query"
      />
      <button class="btn btn-primary" @click="doSearch">Cerca</button>
    </div>
    <div class="row">
      <div class="col-6 card" v-for="film in films" :key="film.id">
        <p>{{ film.title }}</p>
        <p>{{ film.original_title }}</p>
        <p>{{ film.original_language }}</p>
        <p>{{ film.vote_average }}</p>
      </div>
    </div>
  </div>
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
      query: "",
      films: [],
    };
  },
  methods: {
    doSearch() {
      const params = {
        query: this.query,
        api_key: this.apiKey,
        language: "it-IT",
      };

      axios
        .get(this.apiURL, { params })
        .then((risp) => {
          this.films = risp.data.results;
          console.log(this.films);
        })
        .catch((err) => console.log(err));
    },
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
