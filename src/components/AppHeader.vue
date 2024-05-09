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
    <div class="container-fluid mt-5">
        <div class="row justify-content-between border">
            <div class="col"></div>
            <div class="col"></div>
            <div class="col">
                <input type="text" v-model="store.searchQuery">
                <button @click="$emit('clicked')" v-on:keyup.enter="$emit('keyup')">Cerca</button>
            </div>
        </div>
    </div>

</template>

<style lang="scss"></style>