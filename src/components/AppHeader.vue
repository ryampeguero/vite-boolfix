<script>
import { store } from "../store.js";
export default {
    data() {
        return {
            store,
        }
    }
}
</script>

<template>
    <input type="text" v-model="store.searchQuery">
    <button @click="$emit('clicked')">Cerca</button>
</template>

<style lang="scss"></style>