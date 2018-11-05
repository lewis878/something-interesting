<template>
  <div class="container" ref="container">
    <div v-for="item,index in 100"
         :style="{left:`${index%10*10}%`,top:`${~~(index/10)*10}%`,backgroundPosition:`-${index%10*100}% -${~~(index/10)*100}%`}"
         @mouseenter="fn1"
         @mouseleave="fn2"
    ></div>
  </div>
</template>

<script>
  export default {
    name: "demo",
    methods: {
      fn1(e) {
        e.target.style.opacity = 1
        e.target.style.transform = `scale(1.3)`
        e.target.style.zIndex = 100
      },
      fn2(e) {
        e.target.style.transform = ``
        e.target.style.zIndex = 0
      }
    }
  }
</script>

<style lang="scss">
  * {
    margin: 0;
    padding: 0;
  }

  html, body {
    width: 100%;
    height: 100%;
  }

  .container {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: #ccc;
    overflow: hidden;
    > div {
      position: absolute;
      width: 10%;
      height: 10%;
      border: 1px solid #fff;
      box-sizing: border-box;
      background: url("./img/1.jpg");
      background-size: 1000% 1000%;
      opacity: 0.5;
      transition: all 0.3s ease;
    }
  }
</style>
