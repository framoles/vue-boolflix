<template>
  <main>
    <h1>FILM</h1>
    <div id="film">
      <CardFilm v-for="(item, index) in filmList" :card="item" :key="index" />
    </div>
    <h1>SERIES</h1>
    <div id="series">
      <CardSeries
        v-for="(item, index) in serieList"
        :card="item"
        :key="index"
      />
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