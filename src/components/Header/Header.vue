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
    { name: 'Home', path: '/' },
    { name: 'The Game', path: '/game' },
    { name: 'Instructions', path: '/instrucitons' },
    { name: 'About us', path: '/about-us' }
  ];
}
</script>

<style lang="scss">
  #nav {
    padding: 10px;
    background-color: rgb(38, 38, 38);

    ul {
      display: flex;
      list-style-type: none;

      li {
        flex: auto;

        a {
          font-weight: bold;          
          color: white;
          text-decoration: none;

          &.router-link-exact-active {
            color: #42b983;
          }
        }
      }
    }
  }
</style>