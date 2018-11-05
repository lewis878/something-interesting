<template>
  <div class="slide-container">
    <div class="banners">
      <a href="" v-for="item in imgUrl">
        <img :src="item">
      </a>
    </div>
    <div class="dots">
      <span class="dot" :class="{active:index === currentIndex}" v-for="(item,index) in imgUrl.length"
            @click="changeIndex(index)"></span>
    </div>
    <div class="ctrl">
      <span class="prev" @click="prev">&lt;</span>
      <span class="next" @click="next">&gt;</span>
    </div>
  </div>
</template>

<script>
  import $ from 'jquery'

  export default {
    name: "slide",
    data() {
      return {
        imgUrl: [
          require('./img/1.jpg'),
          require('./img/2.jpg'),
          require('./img/3.jpg'),
          require('./img/4.jpg'),
          require('./img/5.jpeg')
        ],
        currentIndex: 0,
        canClick: true
      }
    },
    created() {
      this.$width = 800
    },
    mounted() {
      this.autoPlay()
      $('.slide-container').hover(() => {
        clearInterval(this.timer)
      }, () => {
        this.autoPlay()
      })
    },
    methods: {
      next() {
        if (!this.canClick) {
          return
        }
        this.canClick = false
        $('.banners>a').eq(this.currentIndex).animate({
          left: -this.$width
        })
        this.currentIndex++
        if (this.currentIndex >= this.imgUrl.length) {
          this.currentIndex = 0
        }
        $('.banners>a').eq(this.currentIndex).css({
          left: this.$width
        }).animate({
          left: 0
        }, () => {
          this.canClick = true
        })
      },
      prev() {
        if (!this.canClick) {
          return
        }
        this.canClick = false
        $('.banners>a').eq(this.currentIndex).animate({
          left: this.$width
        })
        this.currentIndex--
        if (this.currentIndex < 0) {
          this.currentIndex = this.imgUrl.length - 1
        }
        $('.banners>a').eq(this.currentIndex).css({
          left: -this.$width
        }).animate({
          left: 0
        }, () => {
          this.canClick = true
        })
      },
      changeIndex(index) {
        if (this.currentIndex === index || !this.canClick) {
          return
        }
        this.canClick = false
        if (index > this.currentIndex) {
          $('.banners>a').eq(this.currentIndex).animate({
            left: -this.$width
          })
          $('.banners>a').eq(index).css({
            left: this.$width
          }).animate({
            left: 0
          }, () => {
            this.canClick = true
          })
        } else if (index < this.currentIndex) {
          $('.banners>a').eq(this.currentIndex).animate({
            left: this.$width
          })
          $('.banners>a').eq(index).css({
            left: -this.$width
          }).animate({
            left: 0
          }, () => {
            this.canClick = true
          })
        }
        this.currentIndex = index
      },
      autoPlay() {
        clearInterval(this.timer)
        this.timer = setInterval(() => {
          this.next()
        }, 3000)
      }
    }
  }
</script>

<style lang="scss">

  $width: 800px;

  * {
    margin: 0;
    padding: 0;
  }

  .slide-container {
    position: relative;
    width: $width;
    height: $width*0.4;
    margin: 100px auto 0;
    border: 2px solid red;
    overflow: hidden;
    .banners {
      position: relative;
      width: 100%;
      height: 100%;
      a {
        position: absolute;
        top: 0;
        left: $width;
        width: 100%;
        height: 100%;
        &:first-child {
          left: 0;
        }
        img {
          width: 100%;
        }
      }
    }
    .dots {
      position: absolute;
      bottom: 10px;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      .dot {
        width: 16px;
        height: 16px;
        background: #fff;
        margin-right: 10px;
        transition: width 0.3s ease;
        cursor: pointer;
        &.active {
          background: red;
          width: 28px;
        }
        &:last-child {
          margin-right: 0;
        }
        border-radius: 8px;
      }
    }
    .ctrl {
      span {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        width: 30px;
        height: 60px;
        text-align: center;
        line-height: 60px;
        background: rgba(0, 0, 0, 0.6);
        color: #fff;
        cursor: pointer;
        user-select: none;
      }
      .prev {
        left: 0;
      }
      .next {
        right: 0;
      }
    }
  }
</style>
