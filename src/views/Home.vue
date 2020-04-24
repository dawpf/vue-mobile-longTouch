<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <div @touchstart="gotouchstart" @touchmove="gotouchmove" @touchend="gotouchend" class="div">按钮</div>
  </div>
</template>

<script>
export default {
  data() {
    return {}
  },
  methods: {
    // 手指按下事件
    gotouchstart() {
      window.isClick = true
      clearTimeout(this.timeOut)
      this.timeOut = setTimeout(function() {
        console.log('在这里执行长按事件')
        window.isClick = false
      }, 500)
    },
    //手释放，如果在500毫秒内就释放，则取消长按事件，此时可以执行onclick应该执行的事件
    gotouchend() {
      clearTimeout(this.timeOut)

      if (window.isClick) {
        console.log('在这里执行点击事件')
      }
    },
    //如果手指有移动，则取消所有事件，此时说明用户只是要移动而不是长按
    gotouchmove() {
      // console.log('手指移动了')
      clearTimeout(this.timeOut)
      window.isClick = false
    }
  },
  // 项目销毁前清除定时器
  beforeDestroy() {
    clearTimeout(this.timeOut)
  }
}
</script>

<style scoped>
.div {
  margin: 0 auto;
  width: 100px;
  height: 100px;
  line-height: 100px;
  border: 1px solid #000;
}
</style>
