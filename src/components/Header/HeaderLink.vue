<template>
    <li>
        <router-link :to="data.path">{{data.name}}</router-link>
    </li>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import HeaderLink from "@/types/HeaderLink";

@Component
export default class Header extends Vue {
    @Prop() private data!: HeaderLink;
}
</script>