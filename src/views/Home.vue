<template>
  <div class="home">
    <div class="container">
      <h1>Welcome to the "Concentration Game"</h1>
      <p>Read the instructions before playing and have a good time!</p>
      <span>Created by Emīls Cinītis as a test for "Picanova Baltics"</span>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class Home extends Vue {}
</script>

<style lang="scss" scoped>
  .home {
    margin: 10% auto 0;
    max-width: 90%;

    h1 {
      margin-top: 0;
    }

    p {
      font-size: 20px;
    }

    span {
      display: block;

      margin-top: 60px;

      font-size: 14px;
      text-align: right;
    }
  }
</style>
