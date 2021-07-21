<style lang="less" scoped>
.homeBox{
  width: 500px;
  height: 600px;
  border: 1px solid black;

}
.home {
 
  margin: auto;
  // text-align: center;
  display: flex;
  justify-content: center;
  input {
    width: 200px;
    height: 30px;
    border: 1px solid black;
    text-indent: 6px;
    // font-size: 16px;
  }
  .button {
    width: 40px;
    height: 32px;
    border: 1px solid gray;
    background: lightblue;
    border-left: none;
    text-align: center;
    line-height: 32px;
    > i {
      color: white;
      font-size: 20px;
    }
  }
}
main{
  .el-table-column{
    text-align: center;
  }
}
</style>
<template>
  <div class="homeBox">
    <div class="home">
      <input
        type="text"
        placeholder="请输入要查询的城市"
        v-model="city"
        @keyup.enter="search"
      />
      <div class="button" @click="search">
        <i class="el-icon-search"></i>
      </div>
    </div>
    <main>

      <el-table
    
    style="width: 100%">
    <el-table-column type="expand">
      <template>
        <el-form label-position="left" inline class="demo-table-expand">
          <el-form-item label="date">
            <span>{{ list.date }}</span>
          </el-form-item>
          <!-- <el-form-item label="风级">
            <span>{{  }}</span>
          </el-form-item>
          <el-form-item label="风向">
            <span>{{  }}</span>
          </el-form-item>
          <el-form-item label="高温">
            <span>{{  }}</span>
          </el-form-item>
          <el-form-item label="低温">
            <span>{{  }}</span>
          </el-form-item>
          <el-form-item label="天气类型">
            <span>{{  }}</span>
          </el-form-item>
           -->
        </el-form>
      </template>
    </el-table-column>
    <el-table-column
      label="城市"
      :prop="citys">
    </el-table-column>
    <el-table-column
      label="温度"
      :prop="wendu">
    </el-table-column>
    <el-table-column
      label="感冒"
      :prop="ganmao">
    </el-table-column>
  </el-table>
    </main>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      city: "",
      citys:"",
      wendu:"",
      ganmao:"",
      list:[],

       tableData: [{
          // id: '12987122',
          name: '好滋好味鸡蛋仔',
          category: '江浙小吃、小吃零食',
          desc: '荷兰优质淡奶，奶香浓而不腻',
          address: '上海市普陀区真北路',
          shop: '王小虎夫妻店',
          shopId: '10333'
        }, {
          // id: '12987123',
          name: '好滋好味鸡蛋仔',
          category: '江浙小吃、小吃零食',
          desc: '荷兰优质淡奶，奶香浓而不腻',
          address: '上海市普陀区真北路',
          shop: '王小虎夫妻店',
          shopId: '10333'
        }, {
          // id: '12987125',
          name: '好滋好味鸡蛋仔',
          category: '江浙小吃、小吃零食',
          desc: '荷兰优质淡奶，奶香浓而不腻',
          address: '上海市普陀区真北路',
          shop: '王小虎夫妻店',
          shopId: '10333'
        }, {
          // id: '12987126',
          name: '好滋好味鸡蛋仔',
          category: '江浙小吃、小吃零食',
          desc: '荷兰优质淡奶，奶香浓而不腻',
          address: '上海市普陀区真北路',
          shop: '王小虎夫妻店',
          shopId: '10333'
        }]
      
    };
  },
  methods: {
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
        console.log(this.citys);
        this.wendu = res.data.data.wendu;
        this.ganmao = res.data.data.ganmao;
        this.list = res.data.data.forecast[0];
        console.log(this.list,"list");
      });
    },
  },
  created() {
    // this.search();
  },
};
</script>
