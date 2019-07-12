<template>
  <div>
    <table>
      <thead>
      <tr>
        <th>name</th>
        <th>age</th>
        <th>like</th>
        <th>sex</th>
      </tr>
      </thead>
      <tbody v-for="(item, i) in tableData" :key="i">
      <tr>
        <td v-for="(value, key) in item" :key="key">
          <!-- is="t-item" 去掉多渲染的表格边框-->
          <span is="t-item">{{value}}</span>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
  export default {
    name: "table",
    data() {
      return {
        tableData: []
      }
    },
    // 接收父组件传值
    props: ["tabledata"],
    mounted() {
      this.tableInit();
    },
    methods: {
      tableInit: function() {
        this.clearData();
        this.tableData = this.tabledata;
        // 强制刷新方法
        this.$nextTick(() => {
          this.tableData = this.tabledata;
        });
        console.log("yes");
      },
      clearData: function() {
        this.tableData = [];
      }
    }
  }
</script>
<style scoped>
  table {
    border-collapse: collapse;
  }
  table td,
  table th {
    width: 200px;
    border: 1px #ccc solid;
    padding: 10px 50px;
  }
</style>
