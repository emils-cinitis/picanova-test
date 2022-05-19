<template>
  <header id="nav">
    <ul>
      <template v-for="headerLink in headerLinks">
        <HeaderLink :data="headerLink" v-bind:key="headerLink.path"></HeaderLink>
      </template>
    </ul>
  </header>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HeaderLinkType from "@/types/HeaderLink";
import HeaderLink from "./HeaderLink.vue";

@Component({
  components: {
    HeaderLink
  }
})
export default class Header extends Vue {
  headerLinks: HeaderLinkType[] = [
    { name: 'Home', path: 'home' },
    { name: 'The Game', path: 'game' },
    { name: 'Instructions', path: 'instrucitons' },
    { name: 'About us', path: 'about-us' }
  ];
}
</script>