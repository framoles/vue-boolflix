<template>
  <div>
    <img :src="getSrc(cast.profile_path)" :alt="cast.name" />
    {{ cast.name }}
  </div>
</template>

<script>
export default {
  props: {
    cast: Object,
  },
  methods: {
    getSrc(path) {
      if (path != null) {
        return `https://image.tmdb.org/t/p/original${path}`;
      } else {
        return "https://bit.ly/3rMN9Vs";
      }
    },
  },
};
</script>

<style lang="scss" scoped>
img {
  width: 50px;
}
</style>