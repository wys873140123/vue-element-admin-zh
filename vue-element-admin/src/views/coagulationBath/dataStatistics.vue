<template>
    <div class="page">
        <el-row :gutter="40">
            <el-col :span="14">
                <div class="">
                    <el-select v-model="time" style="margin-right:20px" placeholder="请选择时间">
                        <el-option
                        v-for="item in selectTimeList"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                        </el-option>
                    </el-select>
                    <el-select v-model="line" placeholder="请选择产线">
                        <el-option
                        v-for="item in selectLineList"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                        </el-option>
                    </el-select>
                </div>
                 <div class="table">
                    <div class="table_name">近期报警列表</div>
                    <el-table
                        :data="tableData"
                        stripe
                        style="width: 100%">
                        <el-table-column
                        type="index"
                        label="序号"
                        width="80">
                        </el-table-column>
                        <el-table-column
                        prop="address"
                        label="详细位置"
                        min-width="200"
                        show-overflow-tooltip>
                        </el-table-column>
                        <el-table-column
                        prop="time"
                        label="异常时间"
                        width="200">
                        </el-table-column>
                        <el-table-column
                        prop="name"
                        label="异常名称"
                        width="120"
                        show-overflow-tooltip>
                        </el-table-column>
                        <el-table-column
                        prop="img"
                        label="异常图片"
                        width="100">
                        </el-table-column>
                        <el-table-column
                        label="是否已处理"
                        width="100">
                        <template slot-scope="scope">
                            <span :class="scope.row.state==true?'font_green':'font_red'">{{ scope.row.state==true?'已处理':'未处理' }}</span>
                        </template>
                        </el-table-column>
                    </el-table>
                    <div class="pagination">
                        <el-pagination
                            @size-change="handleSizeChange"
                            @current-change="handleCurrentChange"
                            :current-page="currentPage4"
                            :page-sizes="[10, 20, 30, 40]"
                            :page-size="20"
                            layout="total, sizes, prev, pager, next, jumper"
                            :total="400">
                        </el-pagination>
                    </div>
                        
                </div>
            </el-col>
            <el-col :span="10">
                 <div class="selectGroup1">
                    <el-select v-model="time" style="margin-right:20px" placeholder="请选择时间">
                        <el-option
                        v-for="item in selectTimeList"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                        </el-option>
                    </el-select>
                    <el-select v-model="line" placeholder="请选择产线">
                        <el-option
                        v-for="item in selectLineList"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                        </el-option>
                    </el-select>
                </div>
                <div>
                    <div id="echarts_line1" class="echarts_line" style="height:450px;width:90%"></div>
                </div>
                <div class="selectGroup2">
                    <el-select v-model="time" style="margin-right:20px" placeholder="请选择时间">
                        <el-option
                        v-for="item in selectTimeList"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                        </el-option>
                    </el-select>
                    <el-select v-model="line" placeholder="请选择产线">
                        <el-option
                        v-for="item in selectLineList"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                        </el-option>
                    </el-select>
                </div>
                <div>
                    <div id="echarts_line2" class="echarts_line" style="height:450px;width:90%"></div>
                </div>
            </el-col>
        </el-row>
      
      
    </div>
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'dataStatistics',
  components: { },
  data() {
    return {
        selectTimeList: [{
          value: '1',
          label: '今日'
        }, {
          value: '2',
          label: '本周'
        }, {
          value: '3',
          label: '当月'
        }, {
          value: '4',
          label: '三个月'
        }, {
          value: '5',
          label: '六个月'
        }],
        time: '1',
        selectLineList: [{
          value: '1',
          label: '所有产线'
        }, {
          value: '2',
          label: '1号线'
        }, {
          value: '3',
          label: '2号线'
        }, {
          value: '4',
          label: '3号线'
        }, {
          value: '5',
          label: '4号线'
        }],
        line: '1',
         tableData: [{
          time: '2022-9-27 16:24:46',
          name: '王小虎',
          address: '三号线第三层第四个点位11111111111',
          img:'',
          state:true,
        },{
          time: '2022-9-27 16:24:50',
          name: '王小虎',
          address: '三号线第三层第四个点位',
          img:'',
          state:false,
        },],
         currentPage4: 4
    }
  },
  computed: {
  },
  mounted(){
    this.initChart();
    this.initChart2()
  },
  methods: {
     handleSizeChange(val) {
        console.log(`每页 ${val} 条`);
      },
      handleCurrentChange(val) {
        console.log(`当前页: ${val}`);
      },
      initChart() {
        this.chart = echarts.init(document.getElementById('echarts_line1'))

        this.chart.setOption({
           title: {
              text: '报警趋势图',
              left:'45%'
            },
            tooltip: {
              trigger: 'axis'
            },
            legend: {
              bottom:0,
              data: ['总异常数', '未处理异常']
            },
            grid: {
              left: '3%',
              right: '4%',
              bottom: '10%',
              containLabel: true
            },
            xAxis: {
              type: 'category',
              boundaryGap: false,
              data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
            },
            yAxis: {
              type: 'value'
            },
            series: [
              {
                name: '总异常数',
                type: 'line',
                data: [220, 132, 101, 134, 90, 230, 210]
              },
              {
                name: '未处理异常',
                type: 'line',
                data: [220, 20, 40, 34, 5, 100, 38]
              },
            ]
        })
      },
      initChart2() {
        this.chart = echarts.init(document.getElementById('echarts_line2'))

        this.chart.setOption({
           title: {
              text: '异常项统计',
              left:'45%'
            },
            tooltip: {
              trigger: 'axis',
            },
            legend: {
              bottom:0,
              data: ['断丝', '浆块', '丝束交缠', '残余接头', '纱线粘黏']
            },
            grid: {
              left: '3%',
              right: '4%',
              bottom: '10%',
              containLabel: true
            },
            xAxis: {
              type: 'category',
              boundaryGap: false,
              data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
            },
            yAxis: {
              type: 'value'
            },
            series: [
              {
                name: '断丝',
                type: 'line',
                data: [220, 132, 101, 134, 90, 230, 210]
              },
              {
                name: '浆块',
                type: 'line',
                data: [220, 182, 191, 234, 290, 330, 310]
              },
              {
                name: '丝束交缠',
                type: 'line',
                data: [150, 232, 201, 154, 190, 330, 410]
              },
              {
                name: '残余接头',
                type: 'line',
                data: [320, 332, 301, 334, 390, 330, 320]
              },
              {
                name: '纱线粘黏',
                type: 'line',
                data: [820, 932, 901, 934, 1290, 1330, 1320]
              }
            ]
        })
      }
  },
}
</script>

<style lang="scss" scoped>
    .page{
        padding-left: 40px;
        padding-right: 40rpx;
        padding-top: 20px;
        .table{
            margin-top: 40px;
            .table_name{
                text-align: center;
                font-size: 18px;
                margin-bottom: 20px;
            }
            .font_green{
                color: green;
            }
            .font_red{
                color: red;
            }
            .pagination{
                margin-top: 20px;
            }
        }
        .echarts_line{
          margin-top: 20px;
        }
        .selectGroup1{
          margin-left: 26px;
        }
        .selectGroup2{
          margin-left: 26px;
          margin-top: 20px;
        }
       
    }
</style>
