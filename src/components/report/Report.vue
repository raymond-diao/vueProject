<template>
  <div>
    <!-- 面包屑导航 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>数据统计</el-breadcrumb-item>
      <el-breadcrumb-item>数据报表</el-breadcrumb-item>
    </el-breadcrumb>

    <!-- 卡片视图区 -->
    <el-card>
      <!-- 2 在页面中开辟图表空间 -->
      <div id="main" style="width: 600px; height: 400px"></div>
    </el-card>
  </div>
</template>

<script>
// 1 导入 Echarts
import echarts from 'echarts'

export default {
  data() {},
  created() {},
  // 此时页面的dom元素已经渲染完毕
  async mounted() {
    let echarts = require('echarts')
    // 3 .基于准备好的dom，初始化echarts实例
    var myChart = echarts.init(document.getElementById('main'))

    const {data:res} = await this.$http.get("reports/type/1")
    if(res.meta.status !== 200){
      return this.$message.error('获取折线图数据失败！')
    }

    // 4 准备数据和配置项

    // 5 展示数据
    myChart.setOption(res.data)
  },

  methods: {},
}
</script>


<style lang="less" scoped>
</style>

