<template>
  <div 
    class="card"
    :class="{ removed: data.removed }"
    v-if="!!data" 
    @click="toggleCard"
  >
    <div class="image-wrapper">
      <img
        :class="{ shown: showImage }"
        :src="data.imageUrl" 
        :alt="data.value" 
        v-if="!hideCardData" 
      />
    </div>
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
        }, 900);
      }
    }, 10);
  }
}
</script>

<style lang="scss" scoped>
    .card {
        flex: calc(25% - 4px);
        margin: 2px;

        &.removed {
            transition: opacity 1s linear;
            opacity: 0;
        }

        .image-wrapper {
            position: relative;
            padding-top: 137.333%;
            background-color: white;
            cursor: pointer;

            img {
                position: absolute;
                top: 0;
                left: 0;
                width: 100%;

                transition: transform 1s;
                transform: rotateY(120deg);
                backface-visibility: hidden;

                &.shown {
                    transform: rotateY(0);
                }
            }
        }
    }
</style>