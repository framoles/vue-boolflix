<template>
  <!-- Card immagine + info serie tv-->
  <div class="card" @click="cardIsClicked(card.id)">
    <div class="card-hover">
      {{ card.name }}
      <div v-if="card.name != card.original_name">
        {{ card.original_name }}
      </div>
      <lang-flag :iso="card.original_language" />
      <!-- container del voto in stelle -->
      <div class="vote-container">
        <i
          class="fa-solid fa-star"
          v-for="star in Math.ceil(card.vote_average / 2)"
          :key="star + 'solid'"
        ></i>
        <i
          class="fa-regular fa-star"
          v-for="star in 5 - Math.ceil(card.vote_average / 2)"
          :key="star + 'regular'"
        ></i>
      </div>
      <!-- fine container del voto in stelle -->
      <!-- descrizione serie tv -->
      {{ card.overview }}
    </div>
    <!-- se clicco card mostra gli attori -->
    <div class="cast" v-if="cardClicked">
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
    //calcolo src dinamica dell' immagine serie tv
    getUrl(path) {
      if (path != null) {
        return `https://image.tmdb.org/t/p/original${path}`;
      } else {
        return "https://bit.ly/3rMN9Vs";
      }
    },
    //funzione per chiamare le api del cast di attori
    cardIsClicked(id) {
      this.cardClicked = !this.cardClicked;
      if (id != undefined) {
        if (this.cardClicked) {
          const params = {
            api_key: apiKey,
            language: "it-IT",
          };
          axios
            .get("https://api.themoviedb.org/3/tv/" + id + "/credits", {
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