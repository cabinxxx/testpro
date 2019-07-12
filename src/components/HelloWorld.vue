<template>
  <div>
    <div class="head">
      <input class="inp1" type="text" v-model="value1" placeholder="请输入姓名" />
      <input class="inp2" type="text" v-model="value2" placeholder="请输入性别" />
      <button class="search" @click="searchFunc">查询</button>
    </div>
    <div class="body">
      <Table ref="Table" :tabledata="Tdata"></Table>
    </div>
    <div>
      <!-- 分页组件 -->
      <Pagination :total="totalH" :current-page="current" @pagechange="pagechange"></Pagination>
    </div>
  </div>
</template>
<script>
  import Pagination from "./pubcomponents/pagination"
  import Table from "./pubcomponents/table"
  export default {
    name: "home",
    data() {
      return {
        value1: "", //输入框1的值
        value2: "", //输入框2的值
        totalH: 0, // 记录总条数
        displayH: 0, // 每页显示条数
        current: 1, // 当前的页数
        Tdata: [
          {
            //表格数据
            name: "xx",
            age: 18,
            like: "footbal",
            sex: "male"
          },
          {
            //表格数据
            name: "yy",
            age: 28,
            like: "pingpong",
            sex: "female"
          },
          {
            //表格数据
            name: "zz",
            age: 12,
            like: "footbal",
            sex: "male"
          },
          {
            //表格数据
            name: "ss",
            age: 68,
            like: "run",
            sex: "female"
          }
        ]
      };
    },

    components: {
      Pagination,
      Table
    },
    mounted() {
      //声明周期页面加载完成时执行页面请求函数
      this.pageInit();
    },
    methods: {
      pageInit: function() {
        this.totalH = this.Tdata.length;
      },
      pagechange: function(currentPage) {
        // console.log(currentPage); //该参数就是当前点击的页码数
        // 一般情况是发送axios请求, 向后台发送 currentPage, 来获取对应页的数据
      },
      searchFunc: function() {
        // console.log(this.value1);
        let val1 = this.value1;
        let val2 = this.value2;
        let newArr = [];
        //获取输入框中的值，进行查询
        for (let i = 0; i< this.Tdata.length; i++) {
          if (this.Tdata[i].name === val1) {
            newArr.push(this.Tdata[i]);
          } else if (this.Tdata[i].sex === val2) {
            newArr.push(this.Tdata[i]);
          }
        }

        this.Tdata = newArr;
        console.log(this.Tdata);
        this.$refs.Table.tableInit();
      }
    }
  };
</script>
<style scoped>
  * {
    margin: 0;
  }
  .head {
    margin: 50px 0 50px 150px;
  }
  .inp1,
  .inp2 {
    width: 30%;
    height: 30px;
    margin-right: 100px;
  }
  .search {
    width: 60px;
    height: 30px;
    background-color: #fff;
    color: #000;
    border: 1px #ccc solid;
  }
  .search:hover {
    border: 1px #666 solid;
  }
  .body {
    margin: 0 150px 100px;
    padding-top: 50px;
    border-top: 1px #ccc solid;
  }

</style>
