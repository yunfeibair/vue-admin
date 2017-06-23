<template>
  <section>
    <!--工具条-->
    <el-col :span="24" class="toolbar" style="padding-bottom: 0px;">
      <el-form :inline="true" :model="filters">
        <el-form-item>
          <el-select v-model="value" placeholder="请选择">
            <el-option
                    v-for="item in options"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
            </el-option>
          </el-select>
        </el-form-item>
        <el-form-item>
          <el-input v-model="filters.name" placeholder="派出所名称"></el-input>
        </el-form-item>
        <el-form-item>
            <el-date-picker
                    v-model="value3"
                    type="daterange"
                    placeholder="选择日期范围">
            </el-date-picker>

        </el-form-item>
        <el-form-item>
          <el-button type="primary" v-on:click="getUsers">查询</el-button>
        </el-form-item>
      </el-form>
    </el-col>
    <!--情报分析-->
      <el-col class="toolbar" :span="24">
          <el-row style="margin-bottom: 10px">
              <el-col  :span="12">
                  <div class="panel" id="chartColumn" style="width:100%; height:400px;"></div>
              </el-col>
              <el-col :span="12">
                  <div class="panel" id="chartBar" style="width:100%; height:400px;"></div>
              </el-col>
          </el-row>
      </el-col>
    <!--列表-->
    <el-table :data="users" highlight-current-row v-loading="listLoading" style="width: 100%;">
      <el-table-column type="index" width="60">
      </el-table-column>
      <el-table-column prop="name" label="刑事类" width="120">
      </el-table-column>
      <el-table-column prop="sex" label="治安类" width="100" :formatter="formatSex">
      </el-table-column>
      <el-table-column prop="age" label="救助类" width="100">
      </el-table-column>
      <el-table-column prop="birth" label="纠纷类" width="120">
      </el-table-column>
      <el-table-column prop="addr" label="突发事件类" min-width="180">
      </el-table-column>
      <el-table-column prop="addr" label="违法短信信息类" min-width="180">
      </el-table-column>
      <el-table-column prop="addr" label="事故灾害类" min-width="180">
      </el-table-column>
      <el-table-column prop="addr" label="网络安全类" min-width="180">
      </el-table-column>
    </el-table>

    <!--工具条-->
    <el-col :span="24" class="toolbar">
      <el-pagination layout="prev, pager, next" @current-change="handleCurrentChange" :page-size="20" :total="total" style="float:right;">
      </el-pagination>
    </el-col>
  </section>
</template>

<script>
    import util from '../../common/js/util'
    import NProgress from 'nprogress'
    import { getUserListPage, removeUser, batchRemoveUser, editUser, addUser,LineData } from '../../api/api';
    import echarts from 'echarts'
    require('echarts/theme/macarons');
    import axios from 'axios';
    export default {
        data() {
            return {
                chartColumn:null,
                chartBar:null,
                chartPie:null,
                filters: {
                    name: ''
                },
                users: [],
                total: 0,
                page: 1,
                listLoading: false,
                value3: [new Date(2017, 5, 3), new Date(2017, 5, 10)],
                options: [{
                    value: '选项1',
                    label: '朝阳区分局派出所'
                }, {
                    value: '选项2',
                    label: '海淀区分局派出所'
                }, {
                    value: '选项3',
                    label: '东城区分局派出所'
                }, {
                    value: '选项4',
                    label: '西城区分局派出所'
                }, {
                    value: '选项5',
                    label: '昌平区分局派出所'
                }],
                value: ''
            }
        },
        methods: {
            //性别显示转换
            formatSex: function (row, column) {
                return row.sex == 1 ? '男' : row.sex == 0 ? '女' : '未知';
            },
            handleCurrentChange(val) {
                this.page = val;
                this.getUsers();
            },
            //获取用户列表
            getUsers() {
                let para = {
                    page: this.page,
                    name: this.filters.name
                };
                this.listLoading = true;
                NProgress.start();
                getUserListPage(para).then((res) => {
                    this.total = res.data.total;
                    this.users = res.data.users;
                    this.listLoading = false;
                    NProgress.done();
                });
                this.chartLine = echarts.init(document.getElementById('chartColumn'));
                this.chartLine.setOption({
                    title: {
                        text: '2017年6-3-2017-6-10报警统计',
                        x: 'center',                 // 水平安放位置，默认为左对齐，可选为：
                        y: 'top',
                    },
                    tooltip: {
                        trigger: 'axis'
                    },
                    color:["#20a0ff"],
                    xAxis: {
                        type: 'category',
                        boundaryGap: false,
                        data: ['6-3', '6-4', '6-5', '6-6', '6-7', '6-8', '6-9']
                    },
                    yAxis: {
                        type: 'value'
                    },
                    series: [
                        {
                            name: '报警数',
                            smooth:true,
                            type: 'line',
                            stack: '总量',
                            data: [200, 30, 80, 134, 40, 230, 20]
                        }
                    ]
                });
                this.chartColumn = echarts.init(document.getElementById('chartBar'));
                this.chartColumn.setOption({
                    title: {
                        text: '2017年6-3-2017-6-10报警统计',
                        x: 'center',                 // 水平安放位置，默认为左对齐，可选为：
                        y: 'top',
                    },
                    tooltip: {},
                    xAxis: {
                        data: ["刑侦类", "治安类", "救助类", "纠纷类", "突发类", "信息类"]
                    },
                    yAxis: {},
                    color:["#20a0ff"],
                    series: [{
                        name: '案件数量',
                        type: 'bar',
                        data: [10, 30, 15, 5, 20, 45]
                    }]
                });
            },
            //获取折线图
            drawLineChart() {
                this.chartLine = echarts.init(document.getElementById('chartColumn'));
                this.chartLine.setOption({
                    title: {
                        text: '2017年6-3-2017-6-10报警统计',
                        x: 'center',                 // 水平安放位置，默认为左对齐，可选为：
                        y: 'top',
                    },
                    tooltip: {
                        trigger: 'axis'
                    },
                    color:["#20a0ff"],
                    xAxis: {
                        type: 'category',
                        boundaryGap: false,
                        data: ['6-3', '6-4', '6-5', '6-6', '6-7', '6-8', '6-9']
                    },
                    yAxis: {
                        type: 'value'
                    },
                    series: [
                        {
                            name: '报警数',
                            smooth:true,
                            type: 'line',
                            stack: '总量',
                            data: [120, 132, 101, 134, 90, 230, 210]
                        }
                    ]
                });
            },
            //获取柱状图
            drawColumnChart() {
                this.chartColumn = echarts.init(document.getElementById('chartBar'));
                this.chartColumn.setOption({
                    title: {
                        text: '2017年6-3-2017-6-10报警统计',
                        x: 'center',                 // 水平安放位置，默认为左对齐，可选为：
                        y: 'top',
                    },
                    tooltip: {},
                    xAxis: {
                        data: ["刑侦类", "治安类", "救助类", "纠纷类", "突发类", "信息类"]
                    },
                    yAxis: {},
                    color:["#20a0ff"],
                    series: [{
                        name: '案件数量',
                        type: 'bar',
                        data: [5, 20, 36, 10, 10, 20]
                    }]
                });
            },
        },
        mounted() {
            this.getUsers();
            this.drawLineChart();
            this.drawColumnChart();
        }
    }

</script>

<style scoped>
.content-container{
  padding: 10px;
}
    .panel{
        background: #f2f2f2;
    }
</style>