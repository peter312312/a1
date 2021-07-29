<style lang="less" scoped>
.tab ul {
  width: 80px;
  height: 320px;
  position: fixed;
  top: 25%;
  right: 0px;

  li {
    border: 1px solid black;
    list-style: none;
    background: #c6e2ff;
    text-align: center;
    line-height: 80px;
  }
}
.jiantou {
  position: fixed;
  top: 80%;
  right: 0px;
  width: 80px;
  height: 90px;
  background: #c6e2ff;
  text-align: center;
  line-height: 90px;
  // display: none;
}
</style>
<template>
  <div class="tab">
    <ul v-show="flag">
      <li class="ToTop" @click="toTop(step)">向上</li>
      <li>客服</li>
      <li @click="hide">隐藏</li>
      <li class="ToBottom" @click="toBottom(step)">向下</li>
    </ul>
    <div class="jiantou" @click="display" v-show="!flag">显示</div>
  </div>
</template>
<script>
export default {
  props: {
    step: {
      //此数据是控制动画快慢的
      type: Number,
      default: 60,
    },
  },
  data() {
    return {
      flag: true,
      isActive: false,
      // num : 0
    };
  },
  methods: {
    hide() {
      this.flag = !this.flag;
    },
    display() {
      this.flag = !this.flag;
    },

    toTop(i) {
      //参数i表示间隔的幅度大小，以此来控制速度
      document.documentElement.scrollTop -= i;
      if (document.documentElement.scrollTop > 0) {
        var c = setTimeout(() => this.toTop(i), 16);
      } else {
        clearTimeout(c);
      }
    },
    toBottom(i) {
      var clientHeight =
        document.documentElement.clientHeight || document.body.clientHeight;
      var scrollHeight = document.documentElement.scrollHeight;
      var height = scrollHeight - clientHeight; //超出窗口上界的值就是底部的scrolTop的值
      document.documentElement.scrollTop += i;
      if (document.documentElement.scrollTop < height) {
        var c = setTimeout(() => this.toBottom(i), 16);
      } else {
        clearTimeout(c);
      }
    },
  },
  // created() {
  //   var vm = this;
  //   window.onscroll = function () {
  //     if (document.documentElement.scrollTop > 60) {
  //       vm.isActive = true;
  //     } else {
  //       vm.isActive = false;
  //     }
  //   };
  // },
};
</script>