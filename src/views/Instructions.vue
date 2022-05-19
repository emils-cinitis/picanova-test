<template>
  <div class="instructions">
    <h1>The instructions of the game</h1>
    <ul>
      <li v-for="(item, key) in pageText" v-bind:key="key" >
        <template v-if="typeof item === 'string'">
        {{ item }}
        </template>
        <template v-else>
          {{ item.text }}
          <ul>
            <li v-for="(type, key1) in item.types" v-bind:key="key1" :class="'example-' + key1">
              {{ type }}
            </li>
          </ul>
        </template>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
  import { Component, Vue } from "vue-property-decorator";

  @Component
  export default class Instructions extends Vue {
    data() {
      return {
        pageText: [
          "The game is based on memory and the ability to concentrate.",
          "To play the game you click on one of the cards, which is turned around. When the card is clicked, the face of the card will be revealed. " +
          "Click on another card to reveal the face of another card. If these cards are the same, they will be removed from the board.",
          "The aim of the game is to match all 8 pairs and finish the game in the least amount of moves.",
          { 
            text: "The game's cards consists of a pair of:",
            types: [
              "Ace of Spades",
              "Ten of Spades",
              "Queen of Clubs",
              "Eight of Clubs",
              "King of Hearts",
              "Six of Hearts",
              "Jack of Diamonds",
              "Three of Diamonds"
            ]
          }
        ],
      };
    }
  }
</script>

<style lang="scss" scoped>
  .instructions {
    min-height: calc(100vh - 108px);
    max-width: 55%;
    margin: 0 auto;
    padding-top: 20px;

    @media (max-width: 768px) {
      max-width: 80%;
    }

    h1 {
      margin-top: 0;
    }

    ul {
      padding-left: 0;

      li {
        list-style: none;
        background: url(~@/assets/checkmark.svg) no-repeat left 0;
        background-size: 18px 18px;
        padding-left: 2em;

        text-align: left;
        margin-bottom: 20px;

        ul {
          margin-top: 20px;

          li {
            background-size: contain !important;
            padding-top: 20px;
            padding-bottom: 20px;
            padding-left: 4em;

            @media (min-width: 768px) {
              width: 35%;
              float: left;
            }

            &.example {
              &-0 {
                background: url(~@/assets/cards/1.png) no-repeat left 0;
              }
              &-1 {
                background: url(~@/assets/cards/3.png) no-repeat left 0;
              }
              &-2 {
                background: url(~@/assets/cards/2.png) no-repeat left 0;
              }
              &-3 {
                background: url(~@/assets/cards/4.png) no-repeat left 0;
              }
              &-4 {
                background: url(~@/assets/cards/6.png) no-repeat left 0;
              }
              &-5 {
                background: url(~@/assets/cards/7.png) no-repeat left 0;
              }
              &-6 {
                background: url(~@/assets/cards/5.png) no-repeat left 0;
              }
              &-7 {
                background: url(~@/assets/cards/8.png) no-repeat left 0;
              }
            }
          }
        }
      }
    }
  }
</style>