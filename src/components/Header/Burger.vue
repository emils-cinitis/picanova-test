<template>
  <div class="burger" @click="$emit('burgerOpen')">
    <div class="burger-line burger-line-1"></div>
    <div class="burger-line burger-line-2"></div>
    <div class="burger-line burger-line-3"></div>
  </div>
</template>

<style lang="scss" scoped>
  .burger {
    @media (min-width: 768px) {
        display: none;
    }

    position: relative;
    width: 40px;
    height: 30px;

    .burger-line {
      position: absolute;
      width: 100%;
      height: 4px;
      background-color: white;
      left: 0;

      &-1 {
        top: 0;
      }
      &-2 {
        top: 40%;
      }
      &-3 {
        top: 80%;
      }
    }
  }
</style>