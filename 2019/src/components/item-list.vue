<template>
  <div class="box">
    <div class="box-1">
      <vue-draggable-resizable v-show="!isShow" :parent="true" class="box-2-drag" @resizing="onResize">
        <p class="text-tip" v-show="!showContent">拖放边缘使其与外层重合</p>
        <div class="text-content" v-show="showContent">
          <p class="title">再见，2019！你好，<a href="https://wuufeii.github.io/summary/2020">2020</a></p>
          <p class="content">2019，很美好，有爱；2020会更美好</p>
        </div>
      </vue-draggable-resizable>

    </div>
    <div class="box-2" v-show="isShow">
      <vue-draggable-resizable :resizable="false" :enable-native-drag="true" class="box-2-drag"  @dragging="onDrag">
        <p class="text-tip">拖动此处放入下面矩形中</p>
      </vue-draggable-resizable>
    </div>
  </div>
</template>

<script>
  export default {
    name: "item-list",
    data() {
      return {
        clientWidth: document.documentElement.clientWidth,
        clientHeight: document.documentElement.clientHeight,
        resizable: false,
        isShow: true,
        showContent: false
      }
    },
    methods: {
      onResize (x, y, width, height) {
        let w = (this.clientWidth-16)*0.8
        let h = this.clientHeight*0.4
        if(w - width < 2 && h - height<2) {
          this.showContent = true
        } else {
          this.showContent = false
        }
      },
      onDrag (x, y) {
        let w = this.clientWidth*0.8/2-100
        let h = (this.clientHeight)*0.35-y
        if((w-Math.abs(x)>0)&&(h<0)) {
          this.resizable = true
          this.isShow = false
        } else {
          this.resizable = false
          this.isShow = true
        }
      }
    }
  }
</script>

<style scoped>
  @import url("https://fonts.googleapis.com/css?family=Finger+Paint");
  .box {
    position: relative;
    font-family: "Finger Paint", cursive;
    user-select:none;
  }
  .box-1 {
    position: absolute;
    width: 80%;
    height: 40vh;
    min-height: 200px;
    border: 2px solid #57a3f3;
    top: 50vh;
    left: 10%;
  }
  .box-2 {
    position: absolute;
    top: 15vh;
    left: calc(50% - 100px);
  }
  .box-2-drag {
    border: 1px solid #fff;
  }
  .text-tip {
    font-size: 16px;
  }
  .text-content>.title {
    font-size: 20px;
    font-weight: bold;
    text-align: center;
  }
  .text-content>.content {
    font-size: 16px;
    text-indent: 32px;
  }
</style>
<style>
  .box .handle {
    width: 25px;
    height: 25px;
    background-color: #c8ebcc;
    border-color: #fff;
  }
</style>