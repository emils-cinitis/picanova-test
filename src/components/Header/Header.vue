<template>
  <header>
    <Burger @burgerOpen="toggleNavigation"></Burger>
    <ul :class="{ 'open-mobile': navigationOpen }">
      <CloseBurger @burgerClose="toggleNavigation"></CloseBurger>
      <HeaderLink
        :data="headerLink"
        v-bind:key="headerLink.path"
        v-for="headerLink in headerLinks"
      ></HeaderLink>
    </ul>
  </header>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HeaderLinkType from "@/types/HeaderLink";
import HeaderLink from "./HeaderLink.vue";
import Burger from "./Burger.vue";
import CloseBurger from "./CloseBurger.vue";

@Component({
  components: {
    HeaderLink,
    Burger,
    CloseBurger,
  },
})
export default class Header extends Vue {
  private headerLinks: HeaderLinkType[] = [
    { name: "Home", path: "/" },
    { name: "The Game", path: "/game" },
    { name: "Instructions", path: "/instructions" },
    { name: "About us", path: "/about-us" },
  ];
  private navigationOpen = false;

  toggleNavigation(): void {
    this.navigationOpen = !this.navigationOpen;
  }
}
</script>

<style lang="scss">
header {
  padding: 10px;
  background-color: rgb(38, 38, 38);

  @media (max-width: 768px) {
    padding: 20px 10px;
  }

  ul {
    @media (max-width: 768px) {
      &:not(.open-mobile) {
        left: -1000px;
      }

      transition: left 150ms linear;

      display: block;
      position: absolute;
      top: 0;
      left: 0;
      width: calc(100% - 100px);
      max-width: 1000px;

      background-color: rgb(38, 38, 38);

      padding: 40px 50px 20px;
      margin: 0;

      z-index: 1;

      li {
        font-size: 26px;
        margin-bottom: 20px;
      }
    }

    display: flex;
    list-style-type: none;
    max-width: 500px;
    margin: 1em auto;

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
