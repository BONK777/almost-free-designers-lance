<template>
    <div class="wrapper">
        <main-header/>
        <div class="wrapper">
            <router-view @showPopup="$emit('showPopup')" :userData="userData"></router-view>
        </div>
    </div>
</template>

<script>
import Header from "../Header/index.vue";

export default {
    name: "main-container",
    components: { "main-header": Header },
    props: ["userData"],
}
</script>

<style>
    .wrapper {
        min-height: calc(100vh - 100px);
        box-sizing: border-box;
        background: #23242a;
    }
</style>