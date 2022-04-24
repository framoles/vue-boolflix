<template>
  <header>
    <div id="left">
      <img src="../assets/img/netflix-logo.png" alt="logo" />
      <ul>
        <li>Home</li>
        <li>Film</li>
        <li>Serie TV</li>
      </ul>
    </div>
    <div id="right">
      <input
        type="text"
        placeholder="Cerca"
        v-model="userQuery"
        @keyup.enter="doSearch"
      />
      <button @click="doSearch">Cerca</button>
    </div>
  </header>
</template>

<script>
export default {
  name: "HeaderComponent",
  data() {
    return {
      userQuery: "",
    };
  },
  methods: {
    doSearch() {
      this.$emit("input", this.userQuery);
      this.userQuery = "";
    },
  },
};
</script>

<style lang="scss" scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: rgb(53, 53, 53);
  #left {
    display: flex;
    img {
      width: 100px;
      margin-right: 2em;
    }
    ul {
      display: flex;
      align-items: center;
      column-gap: 3em;
      li {
        list-style: none;
        color: white;
      }
    }
  }
  #right {
    padding: 10px;
    input,
    button {
      font-size: 1em;
      border: none;
      outline: none;
      color: white;
      padding: 10px;
    }
    input {
      background-color: rgb(37, 37, 37);
    }
    button {
      background-color: rgb(131, 131, 131);
      color: white;
      &:hover {
        background-color: rgb(78, 71, 71);
        transition: 300ms;
        cursor: pointer;
      }
    }
  }
}
</style>