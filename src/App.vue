<template>
  <div id="app">
    <Header @input="doSearch" />
    <Main :filmList="filmList" :serieList="serieList" />
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/HeaderComponent.vue";
import Main from "./components/MainComponent.vue";

export default {
  name: "App",
  components: {
    Header,
    Main,
  },
  data() {
    return {
      apiURL: "https://api.themoviedb.org/3/search/",
      apiKey: "5ec423d0e09c1c7875d6ca5bd8343d0a",
      filmList: [],
      serieList: [],
    };
  },
  methods: {
    doSearch(text) {
      if (text.trim() != "") {
        this.callAxios(text, "movie");
        this.callAxios(text, "tv");
      } else {
        alert("nessun testo nella ricerca");
      }
    },

    callAxios(query, mode) {
      const params = {
        query: query,
        api_key: this.apiKey,
        language: "it-IT",
      };

      axios
        .get(this.apiURL + mode, { params })
        .then((risp) => {
          if (risp.status === 200) {
            if (mode == "movie") {
              this.filmList = risp.data.results;
              console.log(this.filmList);
            } else {
              this.serieList = risp.data.results;
              console.log(this.serieList);
            }
          }
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}
</style>
