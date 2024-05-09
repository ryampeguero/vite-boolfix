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
        }
    },

    created() {
        if (this.tvInfo !== undefined || this.movieInfo !== undefined) {
            this.title = (this.isMovie) ? this.movieInfo.title : this.tvInfo.name;
            this.ogTitle = (this.isMovie) ? this.movieInfo.original_title : this.tvInfo.original_name;
            this.ogLang = (this.isMovie) ? this.fixFlags(this.movieInfo.original_language) : this.fixFlags(this.tvInfo.original_language);
            this.rate = this.transformVote((this.isMovie) ? this.movieInfo.vote_average : this.tvInfo.vote_average);
            this.poster = (this.isMovie) ? this.movieInfo.poster_path : this.tvInfo.poster_path;

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
        <div class="mycard text-center">
            <img :src="getBackImage(poster)" alt="">

            <div>
                {{ this.title }}
            </div>
            <div v-if="isTitleRepeated">
                {{ ogTitle }}
            </div>

            <div>
                <span :class="`fi fi-${ogLang}`"></span>
            </div>

            <div>
                <i v-for="index in rate" class="fa-solid fa-star"></i>
                <i v-for="index in 5 - rate" class="fa-regular fa-star"></i>

            </div>

        </div>
    </div>
</template>

<style lang="scss">
.mycard {
    // padding: 10px;
    margin-bottom: 5px;
    min-height: 150px;
    border: 1px solid black;

    img {
        min-width: 100%;
        max-width: 100%;

        min-height: 100%;
        max-height: 100%;
    }
}
</style>