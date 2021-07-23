<style lang="less" scoped>
.homeBox {
  width: 500px;
  // height: 600px;
  border: 1px solid lightblue;
}
.home {
  position: relative;
  .back{
    font-size: 13px;
    color: blue;
    cursor: pointer;
  }
  
}
main {
 
  li{
        list-style-type: none;
      }
}


//active
.aa {
  transition: all 0.2s;
}
.go {
  transform: rotate(90deg);
  transition: all 0.2s;
}
</style>
<template>
  <div class="homeBox">
    <div class="home">
    
      <div class="back" @click="$router.back(-1)">返回</div>
    </div>
    <main>
      
                 <div class="yesterdayDate"> <i @click="handle" :class="['el-icon-arrow-right',rotate ? 'go' : 'aa']"></i> 昨日:7月{{yesterdayData.date}}</div>
                <ul class="yesterdayContent" v-show="isShow">
                  <li>风力:{{yesterdayData.fl}}</li>
                  <li>风向:{{yesterdayData.fx}}</li>
                  <li>高温:{{gaowen}}</li>
                  <li>低温:{{diwen}}</li>
                  <li>类型:{{yesterdayData.type}}</li>
                </ul>
             
            

      
    </main>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      rotate:false,
      isShow:false,
      city: "",
      gaowen:"",
      diwen:"",
      yesterdayData:{}
    };
  },
  methods: {
    // back(){
    //   this.$router.history.go(-1);
    // },
  //箭头
    handle() {
      this.rotate = !this.rotate;
      this.isShow = !this.isShow
      console.log(this.$route,"rrrrrrrrrrrr");
      let na = this.$route.params.citys
      this.axios({
        method: "get",
        url: "/api",
        params: {
          city:na
        },
      }).then((res) => {
        this.yesterdayData = res.data.data.yesterday;
        this.gaowen = res.data.data.yesterday.high.split(" ")[1];
        this.diwen = res.data.data.yesterday.low.split(" ")[1];
      });
    },
  },
  created() {
    // this.handle();
  },
};
</script>
