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

  checkBoard(cardID: number): void {
    this.canShowCard = false;
    const currentlySelectedCardKey = this.getSelectedCardById(cardID);
    const currentlySelectedCard = this.cards[currentlySelectedCardKey];

    if (this.selectedCard !== -1) {
      const oldSelectedCardKey = this.getSelectedCardById(this.selectedCard);
      const oldSelectedCard = this.cards[oldSelectedCardKey];

      if (oldSelectedCard.value === currentlySelectedCard.value) {
        // 
        setTimeout(() => {
          this.cards[oldSelectedCardKey].removed = true;
          this.cards[currentlySelectedCardKey].removed = true;

          this.selectedCard = -1;
          this.canShowCard = true;
        }, 1000);

      } else {
        //
        setTimeout(() => this.hideCards(), 2000);
      }
    } else {
      this.selectedCard = currentlySelectedCard?.id || 0;
      this.canShowCard = true;
    }
  }

  getSelectedCardById(id: number): number {
    let selectedCardKey = -1;
    
    this.cards.forEach((card, key) => {
      if (card.id === id) {
        selectedCardKey = key;
      }
    });

    return selectedCardKey;
  }

  hideCards(): void {
    this.cards.forEach((card) => {
        if (card.shown) {
          card.shown = false;
        }
    });

    this.selectedCard = -1;
    this.canShowCard = true;
  }
}
</script>

<style lang="scss" scoped>
    .field {
        max-width: 328px;
        margin: 0 auto;

        display: flex;
        flex-wrap: wrap;
    }
</style>