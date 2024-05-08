<script>
import { store } from "./store.js";
import axios from "axios";

//Components
import AppHeader from "./components/AppHeader.vue";

export default {
  components:{
    AppHeader,
  },

  data() {
    return {
      store,
    }
  },

  created() {

  },

  methods: {
    callApi() {
      const paramsObj = {
        api_key: store.apiKey,
        query: store.searchQuery,
      };

      let apiUrl = "https://api.themoviedb.org/3/search/movie";
      if (!store.isMovie) {
        apiUrl = "https://api.themoviedb.org/3/search/tv";
      }

      axios.get(apiUrl, { params: paramsObj }).then((resp) => {
        console.log("ciao", resp.data.results);
      });
    }
  }
}
</script>

<template>

  <AppHeader @clicked="callApi"/>

</template>

<style lang="scss"></style>