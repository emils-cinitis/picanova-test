<template>
  <div class="game">
    <template v-if="!showResults">
      <Field
        :cards="allCards"
        @gameFinished="gameFinished"
        @gainedScore="gainedScore"
      ></Field>
      <div class="score-container">
        <span>Score: {{ score }}</span>
      </div>
    </template>
    <div v-else class="results">
      <span>You finished the game in {{ moveCount }} moves!</span>
      <button @click="startNewGame">Start new game</button>
    </div>
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
  private moveCount = 0;
  private score = 0;
  private showResults = false;

  // Preload images so they don't get double loaded afterwards
  private images = [
    require("@/assets/cards/1.png"),
    require("@/assets/cards/2.png"),
    require("@/assets/cards/3.png"),
    require("@/assets/cards/4.png"),
    require("@/assets/cards/5.png"),
    require("@/assets/cards/6.png"),
    require("@/assets/cards/7.png"),
    require("@/assets/cards/8.png"),
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
    this.allCards = this.allCards.sort(() => Math.random() - 0.5);
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

  gainedScore(): void {
    this.score++;
  }

  gameFinished(moveCount: number): void {
    this.resetAllCards();

    this.moveCount = moveCount;
    this.showResults = true;
  }

  resetAllCards(): void {
    this.allCards.forEach((card) => {
      card.shown = false;
      card.removed = false;
    });
  }

  startNewGame(): void {
    this.shuffleCards();
    this.moveCount = 0;
    this.showResults = false;
  }
}
</script>

<style lang="scss" scoped>
.game {
  position: relative;
  height: calc(100vh - 108px);

  display: flex;

  .results {
    position: absolute;
    z-index: 1;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);

    span {
      display: block;
      padding-bottom: 20px;
      font-weight: bold;
      color: black;
    }

    button {
      border: none;
      border-radius: 10px;

      background-color: white;
      padding: 10px 20px;
    }
  }

  .score-container {
    position: absolute;
    top: 20px;
    right: 20px;

    span {
      font-size: 22px;
    }
  }
}
</style>
