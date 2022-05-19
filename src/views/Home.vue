<template>
  <div class="home">
    <div class="container">
      <h1>Welcome to the "Concentration Game"</h1>
      <p>Read the instructions before playing and have a good time!</p>
      <span>Created by Emīls Cinītis as a test for "Picanova Baltics"</span>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .home {
    position: relative;

    max-width: 90%;
    min-height: calc(100vh - 108px);
    margin: 0 auto;

    .container {
      position: absolute;
      width: 100%;
      top: 50%;
      transform: translateY(-50%);

      h1 {
        margin-top: 0;
      }

      p {
        font-size: 20px;
      }

      span {
        display: block;

        margin-top: 60px;

        font-size: 14px;
        text-align: right;

        @media (max-width: 768px) {
          font-size: 10px;
        }
      }
    }
  }
</style>
