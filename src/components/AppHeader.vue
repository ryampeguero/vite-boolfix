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
    <div class="mynavbar">
        <div class="container-fluid pt-2">
            <div class="row justify-content-between p-3">
                <div class="col logo">
                    <h3>BoolFlix</h3>
                </div>
                <div class="col"></div>
                <div class="col d-flex justify-content-end">
                    <input type="text" v-model="store.searchQuery">
                    <button @click="$emit('clicked')">Cerca</button>
                </div>
            </div>
        </div>
    </div>

</template>

<style lang="scss" scoped>
.mynavbar {
    background-color: black;

    .logo {
        color: red;
    }
}
</style>