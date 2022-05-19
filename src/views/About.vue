<template>
  <div class="about">
    <AboutBlock></AboutBlock>
    <div class="text-container">
      <template v-for="(item, key) in tempText">
        <p v-if="typeof item === 'string'" v-bind:key="key">
          {{ item }}
        </p>
        <img v-else :src="item.imageUrl" alt="Person" v-bind:key="key" />
      </template>
    </div>
  </div>
</template>

<script>
import { Component, Vue } from "vue-property-decorator";
import AboutBlock from "@/components/AboutUs/AboutBlock.vue";
@Component({
  components: { AboutBlock }
})
export default class AboutUs extends Vue {
  data() {
    return {
      tempText: [
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit. In aliquam sagittis mauris, eget lacinia tortor blandit eu. Donec eu turpis velit. Nullam tellus odio, hendrerit et euismod nec, luctus condimentum arcu. Vivamus accumsan, eros et tincidunt aliquam, nulla nisi molestie nisi, ut dapibus felis orci eu orci. Duis pretium nulla sit amet tincidunt fermentum. Phasellus sodales velit at arcu tempus consequat. Curabitur eget mauris ut sem pharetra tempus at non risus. Suspendisse scelerisque dui dolor, vel iaculis enim pulvinar eu. Vivamus interdum dapibus leo, sed lobortis ipsum dictum sit amet. Aliquam elementum cursus turpis, ut efficitur ex bibendum ut. Donec in dui porta, sagittis nisl non, porta erat. In hac habitasse platea dictumst. Aenean viverra mattis tellus id iaculis. Mauris diam est, fermentum ut venenatis vel, rutrum quis justo. Curabitur at fringilla massa, ac finibus est. In a sapien ut nunc pulvinar dapibus.",
        { imageUrl: require('@/assets/about-us/person.jpg') },
        "Cras lacinia, libero id facilisis rutrum, purus nibh ultrices metus, sed pellentesque dolor eros sit amet nisi. Integer ac faucibus nunc. Fusce nulla nunc, porta at euismod at, placerat vel elit. In at feugiat erat, pretium condimentum metus. Aliquam ornare rhoncus orci. Phasellus ornare tincidunt imperdiet. Vestibulum aliquet quam facilisis arcu ultricies, faucibus hendrerit magna vehicula. Quisque rhoncus sem nec porttitor congue. Morbi a libero a justo semper blandit sed et lorem.",
        "Phasellus nisi ligula, mollis ac est vel, rutrum iaculis sapien. Quisque id leo euismod, euismod erat sed, varius dui. Vestibulum tempus libero sit amet lorem aliquet scelerisque. Etiam venenatis egestas orci nec lacinia. Nullam id pellentesque nunc. Donec at congue nulla, non varius dui. Sed sit amet urna ligula. Suspendisse eu mauris in tortor lobortis condimentum sed congue eros. Duis convallis magna augue, sit amet facilisis nunc semper sed.",
        "Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Morbi maximus metus euismod urna venenatis congue. Morbi sit amet augue et lectus porttitor pretium. Pellentesque eget facilisis purus, sed eleifend neque. Maecenas pellentesque at metus in consectetur. Pellentesque vulputate pharetra risus nec fringilla. Vivamus ultricies nisl ac erat ultrices cursus. Sed elit ex, dictum vel ante nec, egestas vestibulum lectus. Mauris lacinia augue nec metus fermentum, sit amet tincidunt purus varius. Vivamus ut commodo enim. Quisque porta, orci et dictum consequat, magna magna ullamcorper nunc, quis scelerisque lorem quam ut tortor. Vivamus a eleifend ipsum. Curabitur id velit pellentesque, ultrices enim quis, porta velit. Etiam libero mi, luctus nec lacus ut, rhoncus dapibus ex. Nam cursus urna augue, a venenatis augue blandit non."
      ]
    };
  }
}
</script>

<style lang="scss" scoped>
  .about {
    min-height: calc(100vh - 108px);
    .text-container {
      width: 50%;
      margin: auto;

      @media (max-width: 768px) {
        width: 80%;
      }

      p {
        font-size: 14px;
        font-weight: 300;
        text-align: left;
      }

      img {
        width: 50%;
        max-width: 300px;
        margin: 0 14px 14px 0;

        float: left;

        @media (max-width: 768px) {
          width: 100%; 
          max-width: 100%;
        }
      }
    }
  }
</style>

