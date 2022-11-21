<template>
    <div class="page">
        <el-row :gutter="40">
            <el-col :span="20">
                <div class="">
                   <div class="btn_add">新增缺陷</div>
                </div>
                 <div class="table">
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
                        prop="name"
                        label="缺陷名称"
                        min-width="200"
                        show-overflow-tooltip>
                        </el-table-column>
                        <el-table-column
                        prop="category"
                        label="缺陷分类"
                        min-width="200">
                        </el-table-column>
                        <el-table-column
                        prop="count"
                        label="已产生数量"
                        width="150"
                        show-overflow-tooltip>
                        </el-table-column>                       
                        <el-table-column
                        label="缺陷状态"
                        width="150">
                        <template slot-scope="scope">
                            <span :class="scope.row.state==true?'font_green':'font_red'">{{ scope.row.state==true?'启用':'未启用' }}</span>
                        </template>
                        </el-table-column>
                         <el-table-column
                        label="缺陷状态管理"
                        width="150">
                        <template slot-scope="scope">
                            <el-switch
                                v-model="scope.row.state">
                            </el-switch>
                        </template>
                        </el-table-column>
                         <el-table-column
                        prop="createPerson"
                        label="创建人"
                        width="250"
                        show-overflow-tooltip>
                        </el-table-column>    
                         <el-table-column
                        prop="createTime"
                        label="创建时间"
                        width="200"
                        show-overflow-tooltip>
                        </el-table-column>    
                         <el-table-column
                        prop="operation"
                        label="操作"
                        width="200"
                        show-overflow-tooltip>
                         <template>
                           <span class="btn_edit font_green">编辑</span>
                           <span class="btn_del font_red">删除</span>
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
            <el-col :span="4">
           
            </el-col>
        </el-row>
      
      
    </div>
</template>

<script>
export default {
  name: 'dataManagemenet',
  components: { },
  data() {
    return {   
         tableData: [{
          name: '缠丝',
          category: 'XXXX',
          count: '99',
          state:true,
          createPerson:"张三",
          createTime:'2022-10-13 09:22:09'
        },{
         name: '缠丝',
          category: 'XXXX',
          count: '99',
          state:false,
          createPerson:"张三",
          createTime:'2022-10-13 09:22:09'
        },],
         currentPage4: 1
    }
  },
  computed: {
  },
  mounted(){
  },
  methods: {
     handleSizeChange(val) {
        console.log(`每页 ${val} 条`);
      },
      handleCurrentChange(val) {
        console.log(`当前页: ${val}`);
      },
      
  },
}
</script>

<style lang="scss" scoped>
    .page{
        padding-left: 40px;
        padding-right: 40rpx;
        padding-top: 20px;
        .btn_add{
            background-color: deepskyblue;
            text-align: center;
            color: white;
            width: 120px;
            height:40px;
            line-height: 40px;
            border-radius: 6px;
            border: none;
            cursor: pointer;
            box-shadow: 1px 1px 1px 1px #dedede;
        }
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
            .btn_edit{
                margin-right: 20px;
                cursor: pointer;
            }
            .btn_del{
                cursor: pointer;
            }
        }
      
       
    }
</style>
