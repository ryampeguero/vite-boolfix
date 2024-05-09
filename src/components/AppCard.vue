<script>

export default {

    data() {
        return {

        }
    },

    props: {
        tvInfo: Object,
        movieInfo: Object,
        isMovie: Boolean,
    },


    created() {
    },

    methods: {

    }
}
</script>

<template>
    <div class="col">
        <div>
            {{ tvInfo }}
            {{ movieInfo }}
            {{ isMovie }}
            <h4>{{ (isMovie) ? movieInfo.title : tvInfo.name }}</h4>
            <h4>{{ (isMovie) ? movieInfo.original_title : tvInfo.original_man }}</h4>
            <h4>{{ (isMovie) ? movieInfo.original_language : tvInfo.original_language }}</h4>
            <h4>{{ (isMovie) ? movieInfo.vote_count : tvInfo.vote_count }}</h4>
        </div>
    </div>
</template>

<style lang="scss"></style>