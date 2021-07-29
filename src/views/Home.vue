<style lang="less" scoped>
*{
  text-decoration: none;
  
}
.homeBox {
  width: 500px;
  // height: 600px;
  border: 1px solid lightblue;
}
.home {
  position: relative;
  margin: auto;
  // text-align: center;
  display: flex;
  justify-content: center;
  .el-input {
    width: 200px;
    // height: 30px;
    // border: 1px solid black;
    // text-indent: 6px;
    // font-size: 16px;
  }
  .button {
    position: absolute;
    top: 2px;
    right: 151px;
    width: 40px;
    background: lightblue;
    text-align: center;
    line-height: 38px;
    > i {
      color: white;
      font-size: 20px;
    }
  }
}
main {
  .el-table-column {
    text-align: center;
  }
  .el-form{
    margin: 20px 0 20px 0;
    border-bottom: .5px dotted lightblue;
    .date{
      font-size: 18px;
      font-weight: 400;
    }
    .dateLab /deep/ .el-form-item__label{
      font-size: 18px;
    }
    .el-form-item{
      .yesterdayDate{
        font-size: 12px;
        color: blue;
        cursor: pointer;
        .el-icon-arrow-right{
          cursor: pointer;
        }
      }
      li{
        list-style-type: none;

      }
     
    }
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
      <!-- <input
        type="text"
        placeholder="请输入要查询的城市"
        v-model="city"
        @keyup.enter="search"
      /> -->
      <el-input type="text" placeholder="请输入要查询的城市" v-model.trim="city" clearable @keyup.enter.native="search" > </el-input>
      <div class="button" @click="search">
        <i class="el-icon-search"></i>
      </div>
    </div>
    <main>
      <el-table style="width: 100%" :data="tableData">

        <!-- 展开 -->
        <el-table-column type="expand">
          <template slot-scope="">
            <el-form>
               <el-form-item label="" class="dateLab">
                 <div class="yesterdayDate" @click="clickLook(citys)"> 点击查看昨日天气</div>
                <!-- <ul class="yesterdayContent" v-show="isShow">
                  <li>风力:{{yesterdayData.fl}}</li>
                  <li>风向:{{yesterdayData.fx}}</li>
                  <li>高温:{{yesterdayData.high}}</li>
                  <li>低温:{{yesterdayData.low}}</li>
                  <li>类型:{{yesterdayData.type}}</li>
                </ul> -->
              </el-form-item>
              
            </el-form>
            <el-form label-position="left" inline class="demo-table-expand" v-for="(item,index) in tableDataAll" :key="index">
              
               <!-- <el-form-item label="昨天:" class="dateLab">
                
              </el-form-item> -->
              
              <el-form-item label="日期:" class="dateLab">
                <span class="date">{{ item.date }}</span>
              </el-form-item>
              <br />
              <el-form-item label="高温:">
                <span>{{ item.high }}</span>
              </el-form-item>
              <br />
              <el-form-item label="低温:">
                <span>{{ item.low }}</span>
              </el-form-item>
              <br />
              <el-form-item label="风向:">
                <span>{{ item.fengxiang }}</span>
              </el-form-item>
              <br />
              <el-form-item label="风力:">
                <span>{{ item.fengli }}</span>
              </el-form-item>
              <br />
              <el-form-item label="类型:">
                <span>{{ item.type }}</span>
              </el-form-item>
            </el-form>
          </template>
        </el-table-column>

        <el-table-column label="城市" width="180">
          <span>{{ citys }}</span>
        </el-table-column>
        <el-table-column label="温度℃" width="180">
          <span>{{ wendu }}</span>
        </el-table-column>
        <el-table-column label="备注" width="180">
          <span>{{ ganmao }}</span>
        </el-table-column>
       
      </el-table>
    </main>
    <!-- <About/> -->
    <div class="copyBox">
      <!-- <button class="btn" @click="btn">copy_target</button> -->
      <span>{{ code }}</span>
       <i 
       class="el-icon-document"
       title="点击复制"
       @click="copyActiveCode($event,code )"/>
    </div>
    <tab></tab>
    <router-link to="/event">
    跳转到Event页面
    </router-link>
    
  </div>
</template>

<script>
import About from './About.vue';
import tab from '../components/tab/Tab';
import Event from '../views/Event'
// import Clipboard 首字母必须为大写   （引入到要使用的组件上即可）
import Clipboard from 'clipboard';


export default {
  components: {
    About,
    tab,
  
  },
  data() {
    return {
      code:111,
      rotate:false,
      isShow:false,
      city: "",
      citys: "",
      wendu: "",
      ganmao: "",
      tableData: [],
      tableDataAll:[],
      yesterdayData:{}
    };
  },
  methods: {
    copyActiveCode(e, text) {
      const clipboard = new Clipboard(e.target, { text: () => text })
      clipboard.on('success', e => {
        this.$message({ type: 'success', message: '复制成功' })
        // 释放内存
        clipboard.off('error')
        clipboard.off('success')
        clipboard.destroy()
      })
      clipboard.on('error', e => {
        // 不支持复制
        this.$message({ type: 'waning', message: '该浏览器不支持自动复制' })
        // 释放内存
        clipboard.off('error')
        clipboard.off('success')
        clipboard.destroy()
      })
      clipboard.onClick(e)
    },


    clickLook(citys){
      this.$router.push(`/about/${citys}`)
    },
    // handle(){
    //   // console.log("11");
    //   this.rotate = !this.rotate;
    //   this.isShow = !this.isShow
    // },
    search() {
      this.axios({
        method: "get",
        url: "/api",
        params: {
          city: this.city,
        },
      }).then((res) => {
        console.log(res, "res");
        this.citys = res.data.data.city;
        // console.log(this.citys);
        this.wendu = res.data.data.wendu;
        this.ganmao = res.data.data.ganmao;
        this.tableData = res.data.data.forecast.splice(0,1);
        // console.log(this.tableData, "tableData");
        this.tableDataAll = res.data.data.forecast;
        // console.log(this.tableDataAll,"this.tableDataAll");
        this.yesterdayData = res.data.data.yesterday;
        // console.log(this.yesterdayData,"this.yesterdayData");
      });
    },
  },
  created() {
    // this.search();
  },
};
</script>
