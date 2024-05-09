<script>
import { store } from "./store.js";
import axios from "axios";

//Components
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";

export default {
  components: {
    AppHeader,
    AppMain,
  },

  data() {
    return {
      store,
    }
  },

  created() {

  },

  methods: {
    callMovieApi() {
      const paramsObj = {
        api_key: store.apiKey,
        query: store.searchQuery,
      };

      const apiUrl = "https://api.themoviedb.org/3/search/movie";

      axios.get(apiUrl, { params: paramsObj }).then((resp) => {
        // console.log("ciao", resp.data.results);
        store.movieList = resp.data.results;

      }).finally(() => {

      });

      this.callTvApi();
    },

    callTvApi() {
      const paramsObj = {
        api_key: store.apiKey,
        query: store.searchQuery,
      };

      const apiUrl = "https://api.themoviedb.org/3/search/tv";

      axios.get(apiUrl, { params: paramsObj }).then((resp) => {
        // console.log("ciao", resp.data.results);
        store.tvList = resp.data.results;
      });


    }
  }
}
</script>

<template>
  <i class="fa-regular fa-star"></i>
  <i class="fa-solid fa-star"></i>
  <AppHeader @clicked="callMovieApi" @keyup="callMovieApi"/>

  <AppMain />

</template>

<style lang="scss"></style>