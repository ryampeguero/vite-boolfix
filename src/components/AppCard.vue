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
        }
    },

    created() {

        console.log(this.movieInfo);

        if (this.tvInfo != undefined && this.movieInfo != undefined )
            this.checkTitles();
    },

    methods: {
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

        getBackImage(imageName){
            return `https://image.tmdb.org/t/p/w342/${imageName}`;
        }

    }
}
</script>

<template>
    <div class="col-3">
        <div class="mycard text-center">
            <img :src="getBackImage((isMovie) ? movieInfo.poster_path : tvInfo.poster_path)" alt="">
            <div>
                {{ (isMovie) ? movieInfo.title : tvInfo.name }}
            </div>
            <div v-if="isTitleRepeated">
                {{ (isMovie) ? movieInfo.original_title : tvInfo.original_man }}
            </div>

            <div>
                <span
                    :class="`fi fi-${(isMovie) ? fixFlags(movieInfo.original_language) : fixFlags(tvInfo.original_language)}`"></span>
            </div>

            <div>
                {{ (isMovie) ? movieInfo.vote_count : tvInfo.vote_count }}
            </div>

            <img src="https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png" alt="">


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