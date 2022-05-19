<template>
  <div 
    class="card"
    :class="{ removed: data.removed }"
    v-if="!!data" 
    @click="toggleCard"
  >
    <img
      :class="{ shown: showImage }"
      :src="data.imageUrl" 
      :alt="data.value" 
      v-if="!hideCardData" 
    />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Watch, Vue } from "vue-property-decorator";
import CardType from "@/types/Card";

@Component
export default class Field extends Vue {
  @Prop() private data!: CardType
  @Prop() private canShowCard!: boolean;

  // Set 2 different variables to show cards turning with an animation
  private showImage = false;
  private hideCardData = true;

  toggleCard() {
    // Toggle / show card if user can make another move and card isn't shown or removed from the board already
    if (this.canShowCard && !this.data.shown && !this.data.removed) {
      this.data.shown = !this.data.shown;
      this.$emit('cardShown', this.data.id);
      this.hideCardData = !this.data.shown;
    }
  }

  @Watch('data.shown')
  onDataChanged(value: boolean) {
    // Timeout is used so the styling animation runs
    // Otherwise the card will have no animation
    setTimeout(() => {
      this.showImage = value;

      if (!value) {
        setTimeout(() => {
          this.hideCardData = true;
        }, 1000);
      }
    }, 10);
  }
}
</script>

<style lang="scss" scoped>
    .card {
        flex: calc(25% - 6px);
        max-width: calc(25% - 6px);
        border: 1px solid black;
        margin: 2px;

        height: 103px;

        &.removed {
            transition: opacity 1s linear;
            opacity: 0;
        }

        img {
            transition: transform 1s;
            transform: rotateY(120deg);
            backface-visibility: hidden;

            &.shown {
                transform: rotateY(0);
            }
        }
    }
</style>