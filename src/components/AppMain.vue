<script>
import {store} from "../store.js";
import AppCard from "./AppCard.vue";

export default {
    components: {
        AppCard,
    },

    data(){
        return {
            store,
        }
    }
}
</script>

<template>
    <!-- Movie Cards -->
    <div class="container">
        <div class="row">
            <div class="col">
                <!-- AppCards & Movies -->
                <div class="container">
                    <h3>Movie Series</h3>
                    <div class="row">
                        <AppCard v-for="movie in store.movieList" :movieInfo="movie" :isMovie="store.isMovie" />
                    </div>

                </div>
                
            </div>
        </div>
    </div>

    <!-- Tv Cards -->
    <div class="container pt-5">
        <div class="row">
            <div class="col">
                <!-- AppCards & Tv -->
                <div class="container">
                    <h3>TV Series</h3>
                    <div class="row">
                        <AppCard v-for="tv in store.tvList" :tvInfo="tv" :isMovie="!store.isMovie"/>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss">

</style>