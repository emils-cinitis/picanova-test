<template>
  <div class="game">
    <Field :cards="allCards"></Field>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Field from "@/components/Game/Field.vue";
import CardType from "@/types/Card";

@Component({
  components: {
    Field,
  },
})
export default class Game extends Vue {
  private gridSize = 16;
  private allCards: CardType[] = [];

  // Preload images so they don't get double loaded afterwards
  private images = [
    require("@/assets/1.png"),
    require("@/assets/2.png"),
    require("@/assets/3.png"),
    require("@/assets/4.png"),
    require("@/assets/5.png"),
    require("@/assets/6.png"),
    require("@/assets/7.png"),
    require("@/assets/8.png"),
  ];

  mounted(): void {
    this.getAllCards();
    this.shuffleCards();
  }

  getAllCards(): void {
    // Cycle all grid size and generate cards
    for (let i = 0; i < this.gridSize; i++) {
      const currentCard = Math.floor(i / 2);
      const imageUrl = this.images[currentCard];

      this.allCards.push(this.generateCard(i, currentCard, imageUrl));
    }
  }

  shuffleCards(): void {
    // Shuffle array of cards
  }

  generateCard(id: number, value: number, imageUrl: string): CardType {
    // Generate card type with given values
    return {
      id: id,
      value: value,
      imageUrl: imageUrl,
      shown: false,
      removed: false,
    };
  }
}
</script>
