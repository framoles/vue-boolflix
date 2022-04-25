<template>
  <main>
    <h1>FILM</h1>
    <!-- stampa array dei film -->
    <div id="film">
      <CardFilm v-for="film in filmList" :card="film" :key="film.id" />
    </div>
    <h1>SERIES</h1>
    <!-- stampa array delle serie tv -->
    <div id="series">
      <CardSeries v-for="serie in serieList" :card="serie" :key="serie.id" />
    </div>
  </main>
</template>

<script>
import CardFilm from "./CardFilm.vue";
import CardSeries from "./CardSeries.vue";

export default {
  name: "MainComponent",
  components: {
    CardFilm,
    CardSeries,
  },
  props: {
    filmList: Array,
    serieList: Array,
  },
};
</script>

<style lang="scss" scoped>
main {
  background-color: rgb(182, 182, 182);
  #film,
  #series {
    width: 80%;
    margin: auto;
    display: flex;
    flex-wrap: wrap;
    gap: 1em;
    padding: 30px;
  }
  h1 {
    text-align: center;
    margin-bottom: 30px;
  }
}
</style>