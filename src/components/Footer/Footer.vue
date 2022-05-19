<template>
    <footer class="footer">
        <span>Version 1.1</span>
        <span>Created by Emils Cinitis</span>
    </footer>
</template>

<script lang="ts">
    import { Component, Vue } from "vue-property-decorator";

    @Component
    export default class Home extends Vue {}
</script>

<style lang="scss" scoped>
    footer {
        position: absolute;
        width: 100%;
        bottom: 0;
        padding: 5px 0;

        background-color: rgb(38, 38, 38);
        span {
            font-size: 12px;
            display: block;
        }
    }
</style>
