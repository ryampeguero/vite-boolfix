<script>

export default {

    props: {
        tvInfo: Object,
        movieInfo: Object,
        isMovie: Boolean,
    },


    data() {
        return {

        }
    },

    created() {
        console.log(this.movieInfo);
        
        console.log(this.fixFlags("en"));
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
        }

    }
}
</script>

<template>
    <div class="col-3">
        <div class="mycard">
            <div>
                {{ (isMovie) ? movieInfo.title : tvInfo.name }}
            </div>
            <div>
                {{ (isMovie) ? movieInfo.original_title : tvInfo.original_man }}
            </div>

            <div>
                {{ (isMovie) ? movieInfo.original_language : tvInfo.original_language }}
            </div>

            <div>
                {{ (isMovie) ? movieInfo.vote_count : tvInfo.vote_count }}
            </div>

            <span :class="`fi fi-${(isMovie) ?  fixFlags(movieInfo.original_language) : fixFlags(tvInfo.original_language) }`"></span>

        </div>
    </div>
</template>

<style lang="scss">
.mycard {
    padding: 10px;
    margin-bottom: 5px;
    min-height: 150px;
    border: 1px solid black;
}
</style>