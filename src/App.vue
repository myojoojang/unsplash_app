<template>
  <div id="container">
    <div class="row">
      <div class="logo space" @click="init">UNSPLASH API DEMO</div>
      <div class="space" />
      <div class="search">
        <input
          placeholder="search"
          class="search-input"
          v-model="searchKeyword"
          @keyup.enter="search"
        />
      </div>
    </div>
    <div class="row">
      <div v-for="el of data" :key="el.id" class="column">
        <card :item="el" />
      </div>
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import axios from "axios";

export default {
  name: "App",

  components: { Card },

  data: () => ({
    data: [],
    searchKeyword: "",
  }),
  created() {
    axios.defaults.headers.common[
      "Authorization"
    ] = `Client-ID ${process.env.VUE_APP_ACCESSKEY}`;

    this.init();
  },

  methods: {
    init() {
      this.searchKeyword = "";
      axios
        .get("https://api.unsplash.com/photos/")
        .then((res) => {
          this.data = res.data;
        })
        .catch((err) => console.error(err));
    },

    search() {
      if (!this.searchKeyword) {
        alert("Please search something!");
        this.init();
        return;
      }
      axios
        .get(
          `https://api.unsplash.com/search/photos/?query=${this.searchKeyword}`
        )
        .then((res) => {
          this.data = res.data.results;
          // console.log(res);
        })
        .catch((err) => console.error(err));
    },
  },
};
</script>

<style lang="scss">
@import "./styles/app.scss";
</style>
