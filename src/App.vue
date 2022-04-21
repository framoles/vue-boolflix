<template>
  <div id="app">
    <div class="input-group w-25">
      <input
        class="form-control"
        type="text"
        placeholder="Cerca"
        v-model="query"
      />
      <button class="btn btn-primary" @click="doSearch">Cerca</button>
    </div>
    <button class="btn btn-primary" @click="(mode = 'movie'), doSearch">
      FILM
    </button>
    <button class="btn btn-primary" @click="(mode = 'tv'), doSearch">
      SERIE TV
    </button>
    <div class="row" v-if="mode == 'movie'">
      <div class="col-5 card" v-for="film in list" :key="film.id">
        <p>{{ film.title }}</p>
        <p>{{ film.original_title }}</p>
        <p>
          {{ film.original_language }}
        </p>
        <p>{{ film.vote_average }}</p>
      </div>
    </div>
    <div class="row" v-if="mode == 'tv'">
      <div class="col-5 card" v-for="film in list" :key="film.id">
        <p>{{ film.name }}</p>
        <p>{{ film.original_name }}</p>
        <p>
          {{ film.original_language }}
        </p>
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
      apiURL: "https://api.themoviedb.org/3/search/",
      apiKey: "5ec423d0e09c1c7875d6ca5bd8343d0a",
      mode: "movie",
      query: "",
      list: [],
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
        .get(this.apiURL + this.mode, { params })
        .then((risp) => {
          if (risp.status === 200) {
            this.list = risp.data.results;
            console.log(this.list);
          }
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
  .card {
    background-image: url("https://image.tmdb.org/t/p/w342/gcr6W7BNNh6XiJjeFdjV3NyeAcs.jpg");
    background-repeat: no-repeat;
  }
}
</style>
