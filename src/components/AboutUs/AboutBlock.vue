<template>
  <div class="about-us-block">
    <span class="header">The story of US</span>
    <span
      >Lorem ipsum dolor sit amet, consectetur adipiscing elit. In aliquam
      sagittis mauris, eget lacinia tortor blandit eu. Donec eu turpis velit.
      Nullam tellus odio, hendrerit et euismod nec, luctus condimentum
      arcu.</span
    >
  </div>
</template>

<style lang="scss" scoped>
.about-us-block {
  background-color: rgb(0, 19, 82);
  padding: 40px 80px;
  border-radius: 0 0 20px 20px;

  @media (max-width: 768px) {
    padding: 30px 40px;
  }

  span {
    display: block;
    max-width: 50%;
    margin: 0 auto;

    line-height: 24px;

    &.header {
      font-size: 30px;
      margin-bottom: 24px;
    }
  }
}
</style>
