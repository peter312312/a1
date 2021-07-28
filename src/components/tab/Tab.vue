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
.jiantou{
    position: fixed;
    top: 80%;
    right: 0px;
    width: 80px;
    height: 90px;
    background: #c6e2ff;
    // display: none;
}
</style>
<template>
  <div class="tab">
    <ul v-show="flag">
      <li>向上</li>
      <li>客服</li>
      <li @click="hide">隐藏</li>
      <li>向下</li>
    </ul>
    <div class="jiantou" @click="display">
        显示
    </div>
  </div>
</template>
<script>
export default {
data(){
    return{
        flag:true
    }

},
methods:{
hide(){
    this.flag = !this.flag
},
display(){
this.flag = !this.flag
}
}
}
</script>