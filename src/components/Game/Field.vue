<template>
  <div class="field" v-if="!!cards">
    <template v-for="(card, key) in cards">
      <Card
        :data="card"
        :canShowCard="canShowCard"
        v-bind:key="key"
        @cardShown="checkBoard"
      ></Card>
    </template>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import Card from "./Card.vue";
import CardType from "@/types/Card";

@Component({
  components: {
    Card,
  },
})
export default class Field extends Vue {
  @Prop() private cards!: CardType[];
  private selectedCard = -1;
  private canShowCard = true;
  private moveCount = 0;

  // Check state of board after move
  checkBoard(cardID: number): void {
    // Dissalow player to click another card
    this.canShowCard = false;

    // Get currently selected card
    const currentlySelectedCardKey = this.getSelectedCardById(cardID);
    const currentlySelectedCard = this.cards[currentlySelectedCardKey];

    if (this.selectedCard !== -1) {
      // Add another move
      this.moveCount++;

      // If there is already a selected card, get new selected card
      const oldSelectedCardKey = this.getSelectedCardById(this.selectedCard);
      const oldSelectedCard = this.cards[oldSelectedCardKey];

      // Check if selected card value is the same as old selected card
      // In other words - are the cards the same
      if (oldSelectedCard.value === currentlySelectedCard.value) {
        this.$emit('gainedScore');
        // Visibly remove cards from the field after 1 second
        setTimeout(() => {
          this.removeCards(oldSelectedCardKey, currentlySelectedCardKey);
          this.checkIfGameDone();
        }, 1000);

      } else {
        // If the cards are not the same, hide them after 2 seconds
        setTimeout(() => this.hideCards(), 2000);
      }
    } else {
      // If this is the first selected card, save it and allow user to select another card
      this.selectedCard = currentlySelectedCard?.id || 0;
      this.canShowCard = true;
    }
  }

  // Get card key in array by card's ID
  getSelectedCardById(id: number): number {
    let selectedCardKey = -1;
    
    this.cards.forEach((card, key) => {
      if (card.id === id) {
        selectedCardKey = key;
      }
    });

    return selectedCardKey;
  }

  checkIfGameDone(): void {
    // Check if game is finished
    let gameFinished = true;

    this.cards.forEach((card) => {
      if (!card.removed) {
        gameFinished = false;
      }
    });

    if (gameFinished) {
      this.$emit('gameFinished', this.moveCount);
    }
  }

  // Soft remove cards from array
  removeCards(key1: number, key2: number): void {
    this.cards[key1].removed = true;
    this.cards[key2].removed = true;

    // Allow user to start new move
    this.selectedCard = -1;
    this.canShowCard = true;
  }

  // Hide shown cards from field
  hideCards(): void {
    this.cards.forEach((card) => {
        if (card.shown) {
          card.shown = false;
        }
    });

    setTimeout(() => {
      // Allow user to start new move
      this.selectedCard = -1;
      this.canShowCard = true;
    }, 900);
  }
}
</script>

<style lang="scss" scoped>
  .field {
    flex: 1;

    max-width: 550px;
    margin: auto;

    display: flex;
    flex-wrap: wrap;
  }
</style>