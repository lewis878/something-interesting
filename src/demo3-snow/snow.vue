<template>
  <div class="snow">
    <div class="mask"></div>
  </div>
</template>

<script>
  export default {
    name: "snow"
  }
</script>

<style lang="scss">
  * {
    margin: 0;
    padding: 0;
  }

  html, body {
    background: #000;
  }

  .mask {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: url("./img/snow1.png") no-repeat, url("./img/snow2.png") no-repeat;
    animation: snow 10s linear infinite;
    pointer-events: none;
  }

  @keyframes snow {
    0% {
      background-position: 0 0, 0 0;
    }
    100% {
      background-position: 1000px 1000px, 500px 500px;
    }
  }
</style>
