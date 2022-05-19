<template>
  <div class="burger" @click="$emit('burgerClose')">
    <div class="burger-line burger-line-1"></div>
    <div class="burger-line burger-line-2"></div>
  </div>
</template>

<style lang="scss" scoped>
.burger {
  @media (min-width: 768px) {
    display: none;
  }

  position: absolute;
  width: 20px;
  height: 20px;

  top: 10px;
  left: 10px;

  .burger-line {
    position: absolute;
    width: 100%;
    height: 4px;
    background-color: white;
    left: 0;
    top: 50%;

    &-1 {
      transform: rotate(45deg);
    }
    &-2 {
      transform: rotate(-45deg);
    }
  }
}
</style>
