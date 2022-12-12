<template>
    <div class="page">
        <el-row :gutter="40">
            <el-col :span="18">
                <div class="">
                  <el-button type="primary">入库</el-button>
                  <el-button type="primary">出库</el-button>
         
                  
                </div>
                 <div class="table">
                    <el-table
                        :data="tableData"
                        stripe
                        border
                        :default-sort = "{prop: 'index', order: 'descending'}"
                        style="width: 100%"
                        height="600"
                        >
                        <el-table-column
                        prop="index"
                        fixed
                        label="序号"
                        sortable
                        align="center"
                        width="80">
                         <template slot-scope="scope">
                            <span>{{ scope.row.index}}层</span>
                        </template>
                        </el-table-column>
                        <el-table-column
                        :label="item.name"
                        min-width="120"
                        v-for="item in titleData" :key="item.index"
                        show-overflow-tooltip>
                        <template slot-scope="scope">
                            <span>{{  scope.row.goods[item.index-1]}}</span>
                        </template>
                        </el-table-column>
                       
                    </el-table>
                                            
                </div>
            </el-col>
            <el-col :span="6">
                    <div class="rightContent">
                        <div class="inputGroup">
                            <div>
                                 <span>行：
                                    <el-input
                                    class="inputStyle"
                                    placeholder="请输入行数"
                                    v-model="line"
                                    :disabled="editFlag">
                                    </el-input>
                                </span>
                            </div>
                            <div>
                                <span>列：
                                    <el-input
                                    class="inputStyle"
                                    placeholder="请输入列数"
                                    v-model="column"
                                    :disabled="editFlag">
                                    </el-input>
                                </span>
                            </div>
                            
                            <el-button type="primary" class="btn_edit" @click="btn_editRow" v-if="editFlag==true">修改</el-button>
                            <el-button type="danger" class="btn_edit" @click="btn_sureRow" v-if="editFlag==false">确认</el-button>
                        </div>                       
                  </div>
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
         tableData: [
            {
                index:'1',
                goods:[
                    {
                        index:'11',
                        name:'书签',
                        count:99
                    },
                    {
                        index:'12',
                        name:'书签',
                        count:99
                    }
                ],

            },
            { 
                index:'2',
                goods:[
                    {
                        index:'21',
                        name:'书签',
                        count:99
                    },
                    {
                        index:'22',
                        name:'书签',
                        count:99
                    }
                ],
            },
        ],
        titleData:[
            {
                index:1,
                name:'第一列'
            }           
         ],
         editFlag:true,
         column:20,
         line:10,
    }
  },
  computed: {
  },
  mounted(){
    this.initTitle();
    this.initTable();
  
  },
  methods: {
      initTitle(){
        this.titleData=[];
        for(let i=0;i<this.column;i++){
            this.titleData.push({
                index:i+1,
                name:'第'+(i+1)+'列'
            })
        }
      },
      initTable(){
        // for(let i=0;i<line;i++){
            
        // }
      },
      btn_editRow(){
        this.editFlag=false;
      },
      btn_sureRow(){
        this.editFlag=true;
      },
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
            .btn_edit{
                margin-right: 20px;
                cursor: pointer;
            }
            .btn_del{
                cursor: pointer;
            }
        }
      .rightContent{
        margin-top: 80px;
        width: 90%;
        border: 1px solid #dfe6ec;
        padding: 20px;
        .inputGroup{
            .inputStyle{
                width: 140px;
                margin-bottom: 20px;
            }
            .btn_edit{
                margin-left: 40px;
                width: 140px;
            }
        }
      }
       
    }
</style>
