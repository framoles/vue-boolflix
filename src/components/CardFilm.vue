<template>
  <!-- se clicco la card film mostra gli attori -->
  <div class="card" @click="cardIsClicked(card.id)">
    <!-- info mostate solo se vado on hover sulla card -->
    <div class="card-hover">
      {{ card.title }}
      <div v-if="card.title != card.original_title">
        {{ card.original_title }}
      </div>
      <lang-flag :iso="card.original_language" />
      <div class="vote-container">
        <i
          class="fa-solid fa-star"
          v-for="(star, index) in Math.ceil(card.vote_average / 2)"
          :key="index"
        ></i>
        <i
          class="fa-regular fa-star"
          v-for="(star, index) in 5 - Math.ceil(card.vote_average / 2)"
          :key="index"
        ></i>
      </div>
      {{ card.overview }}
    </div>
    <div class="cast" v-if="cardClicked">
      <!-- componente che mostra gli attori -->
      <CastCard v-for="cast in castList" :key="cast.id" :cast="cast" />
    </div>
    <img :src="getUrl(card.poster_path)" :alt="card.title" />
  </div>
</template>

<script>
import axios from "axios";
import CastCard from "./CastCard.vue";
import { apiKey } from "../assets/file/api";

export default {
  components: {
    CastCard,
  },
  props: {
    card: Object,
  },
  data() {
    return {
      cardClicked: false,
      castList: [],
    };
  },
  methods: {
    //calcolo dinamico src immagine
    getUrl(path) {
      if (path != null) {
        return `https://image.tmdb.org/t/p/original${path}`;
      } else {
        return "https://bit.ly/3rMN9Vs";
      }
    },
    //chiamata api lista attori
    cardIsClicked(id) {
      this.cardClicked = !this.cardClicked;
      if (id != undefined) {
        if (this.cardClicked) {
          const params = {
            api_key: apiKey,
            language: "it-IT",
          };
          axios
            .get("https://api.themoviedb.org/3/movie/" + id + "/credits", {
              params,
            })
            .then((risp) => {
              for (let i = 0; i < 5; i++) {
                this.castList.push(risp.data.cast[i]);
              }
              console.log(this.castList);
            })
            .catch((err) => console.log(err));
        }
        this.castList = [];
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/file/card-style.scss";
</style>