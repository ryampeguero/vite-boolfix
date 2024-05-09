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
      store.movieList = "";
      const paramsObj = {
        api_key: store.apiKey,
        query: store.searchQuery,
      };

      const apiUrl = "https://api.themoviedb.org/3/search/movie";

      axios.get(apiUrl, { params: paramsObj }).then((resp) => {
        // console.log("ciao", resp.data.results);
        store.movieList = resp.data.results;

      })
      this.callTvApi();
    },

    callTvApi() {
      store.tvList = "";
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
  <AppHeader @clicked="callMovieApi" @keyup.enter="callMovieApi"/>

  <AppMain />

</template>

<style lang="scss" scoped></style>