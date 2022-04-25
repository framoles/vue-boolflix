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
import { apiKey } from "./assets/file/api";

export default {
  name: "App",
  components: {
    Header,
    Main,
  },
  data() {
    return {
      apiURL: "https://api.themoviedb.org/3/search/",
      filmList: [],
      serieList: [],
    };
  },
  methods: {
    //chiamata api dei film e delle serie tv tramite parametro inviato da inputbox in header
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
        api_key: apiKey,
        language: "it-IT",
      };

      //metodo axios per chiamare api medianti certi parametri
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
