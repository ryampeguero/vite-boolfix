<script>

export default {

    props: {
        tvInfo: Object,
        movieInfo: Object,
        isMovie: Boolean,
    },


    data() {
        return {
            isTitleRepeated: false,
            title: "",
            ogTitle: "",
            ogLang: "",
            rate: "",
            poster: "",
            overview: "",
        }
    },

    created() {
        if (this.tvInfo !== undefined || this.movieInfo !== undefined) {
            this.title = (this.isMovie) ? this.movieInfo.title : this.tvInfo.name;
            this.ogTitle = (this.isMovie) ? this.movieInfo.original_title : this.tvInfo.original_name;
            this.ogLang = (this.isMovie) ? this.fixFlags(this.movieInfo.original_language) : this.fixFlags(this.tvInfo.original_language);
            this.rate = this.transformVote((this.isMovie) ? this.movieInfo.vote_average : this.tvInfo.vote_average);
            this.poster = (this.isMovie) ? this.movieInfo.poster_path : this.tvInfo.poster_path;
            this.overview = (this.isMovie) ? this.movieInfo.overview : this.tvInfo.overview;
            // console.log("normale", this.rate);
            // console.warn("arrontodato", Math.floor(parseInt(this.rate) / 2));

        }

        if (this.tvInfo != undefined && this.movieInfo != undefined) {
            console.log(this.tvInfo.poster_path);
            this.checkTitles();
        }
    },

    methods: {
        transformVote(vote) {
            return Math.floor(parseInt(vote) / 2);
        },

        fixFlags(flagName) {
            switch (flagName) {
                case "en":
                    flagName = "gb";
                    break;

                case "ko":
                    flagName = "kr";
                    break;

                case "ja":
                    flagName = "jp";
                    break;

                default:
                    return flagName;
                    break;
            }

            return flagName;
        },

        checkTitles() {
            if (this.movieInfo.original_title !== this.movieInfo.title && this.tvInfo.original_man !== this.tvInfo.name) {
                this.isTitleRepeated = true;
            }
        },

        getBackImage(imageName) {

            if (imageName !== null) {
                return `https://image.tmdb.org/t/p/w342/${imageName}`;
            } else {
                return new URL("../assets/img/blank_poster.jpg", import.meta.url);
            }

        }

    }
}
</script>

<template>
    <div class="col-3">
        <div class="mycard">
            <div class="card-front">
                <img :src="getBackImage(poster)" alt="">
                <!-- <p>ciao</p> -->
            </div>

            <div class="card-back container p-4">
                <div class="row">
                    <div class="col">
                        <span>Titolo: </span>
                        <span class="card-title">{{ this.title }}</span>
                    </div>
                </div>

                <div v-if="isTitleRepeated" class="row">
                    <div class="col">
                        <span>Titolo originale: </span>
                        <span class="card-title">{{ ogTitle }}</span>
                    </div>
                </div>

                <div>
                    <span :class="`fi fi-${ogLang}`"></span>
                </div>

                <div class="row">
                    <div class="col">
                        <span>Voto: </span>
                        <i v-for="index in rate" class="star fa-solid fa-star"></i>
                        <i v-for="index in 5 - rate" class="star fa-regular fa-star"></i>
                    </div>
                </div>

                <div class="row">
                    <div class="col description">
                        <span>Overview: </span>
                        <span class="card-text">{{ overview }}</span>
                    </div>
                </div>

                
                <div class="row mt-2">
                    <div class="col">
                        <span>Attori: </span>
                        <span class="card-text">{{ overview }}</span>
                    </div>
                </div>

            </div>

        </div>
    </div>
</template>

<style lang="scss" scoped>
.mycard {
    // padding: 10px;
    display: flex;
    margin-bottom: 5px;
    min-height: 340px;
    min-width: 150px;

    border: 1px solid black;

    //position relative settata per nascondere il fronte della card
    position: relative;
    top: 0;
    left: 0;
    z-index: 1;

    img {
        min-width: 100%;
        max-width: 100%;

        min-height: 100%;
        max-height: 100%;
    }


}

.card-front {
    &:hover {
        opacity: 0;
        display: none;
    }
}

.card-back {
    position: absolute;
    top: 0px;
    left: 0px;
    z-index: -1;
    // min-height: 100%;
    max-height: 100%;

    min-width: 100%;

    color: white;
    background-color: black;
    font-weight: 600;

    // debug
    // border: 1px solid black;
    overflow-y: auto;

    .star {
        color: gold;
    }

    .card-title, .card-text {
        font-size: 0.8rem;
        font-weight: 400;
    }

    .card-title {
        font-size: 1rem;
    }

    .description {
        max-height: 200px;
        overflow-y: scroll;
        
        // debug
        border-bottom: 0.5px solid white;
    }

    &:hover {
        z-index: 2;
        overflow-y: auto;
    }


}
</style>