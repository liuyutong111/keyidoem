<template>
  <d2-container>
    <!-- <template slot="header">{{$t('page1')}}</template> -->
    <el-row :gutter="20" class="alarm_record alarm_head">
  <el-col :span="6"><div class="grid-content bg-purple">
    设备名称: <el-input v-model="input" placeholder="请输入内容">
    </el-input></div></el-col>
  <el-col :span="6"><div class="grid-content bg-purple">
    设备编号: <el-select v-model="value" placeholder="请选择">
      <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label"
        :value="item.value">
      </el-option>
    </el-select>
    </div></el-col>
  <el-col :span="6"><div class="grid-content bg-purple">
    时间: <el-date-picker
      v-model="value1"
      type="datetime"
      placeholder="选择日期时间">
    </el-date-picker>
    </div></el-col>
  <el-col :span="6"><div class="grid-content bg-purple">
    <el-button type="primary">查询</el-button>
    <el-button plain>重置</el-button>
    </div></el-col>
</el-row>

       <el-table
    ref="multipleTable"
    :data="tableData"
    tooltip-effect="dark"
    style="width: 100%"
    @selection-change="handleSelectionChange">
    <el-table-column
      type="selection"
       align="center"
     >
    </el-table-column>
    <el-table-column
      label="设备名称"
      align="center"
      >
      <template slot-scope="scope">{{ scope.row.date }}</template>
    </el-table-column>
    <el-table-column
      prop="name"
      label="报警方式"
      align="center"
      width="150">
    </el-table-column>
    <el-table-column
      prop="address"
      label="触发条件"
      align="center"
      show-overflow-tooltip>
    </el-table-column>
    <el-table-column
      prop="Processing"
      label="处理状态"
      align="center"
      show-overflow-tooltip>
    </el-table-column>
    <el-table-column
      prop="state_time"
      align="center"
      label="状态更新时间"
      show-overflow-tooltip>
    </el-table-column>
     <el-table-column
      label="操作"
      width="100">
      <template slot-scope="scope">
        <el-button @click="handleClick(scope.row)" type="text" size="small">查看</el-button>
        <el-button type="text" size="small" @click="open">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
  <div class="block">
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage4"
      
      :page-size="100"
      layout=" prev,  pager, next,sizes, jumper"
      :page-sizes="[100, 200, 300, 400]"
      background
      :total="400">
    </el-pagination>
  </div>
  </d2-container>
</template>

<script>
export default {
  name: 'bjrecording',
  data() {
      return {
        currentPage4:4,
        input: '',
        value1:'',
        value:'',
         options: [{
          value: '选项1',
          label: '黄金糕'
        }, {
          value: '选项2',
          label: '双皮奶'
        }, {
          value: '选项3',
          label: '蚵仔煎'
        }, {
          value: '选项4',
          label: '龙须面'
        }, {
          value: '选项5',
          label: '北京烤鸭'
        }],
        tableData: [{
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
          Processing:'已处理',
          state_time:'2019-12-13',
        }, {
          date: '2016-05-02',
          name: '王小虎',
           address: '上海市普陀区金沙江路 1518 弄',
          Processing:'已处理',
          state_time:'2019-12-13',
        }, {
          date: '2016-05-04',
          name: '王小虎',
           address: '上海市普陀区金沙江路 1518 弄',
          Processing:'已处理',
          state_time:'2019-12-13',
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
          Processing:'已处理',
          state_time:'2019-12-13',
        }, {
          date: '2016-05-08',
          name: '王小虎',
           address: '上海市普陀区金沙江路 1518 弄',
          Processing:'已处理',
          state_time:'2019-12-13',
        }, {
          date: '2016-05-06',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
          Processing:'已处理',
          state_time:'2019-12-13',
        }, {
          date: '2016-05-07',
          name: '王小虎',
           address: '上海市普陀区金沙江路 1518 弄',
          Processing:'已处理',
          state_time:'2019-12-13',
        }],
        multipleSelection: []
      }
    },

    methods: {
      // 多选框
      toggleSelection(rows) {
        if (rows) {
          rows.forEach(row => {
            this.$refs.multipleTable.toggleRowSelection(row);
          });
        } else {
          this.$refs.multipleTable.clearSelection();
        }
      },
      handleSelectionChange(val) {
        this.multipleSelection = val;
      },
       handleClick(row) {
        console.log(row);
      },
      //删除
      open() {
        this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning',
          center: true
        }).then(() => {
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });
        });
      },
      handleSizeChange(val) {
        console.log(`每页 ${val} 条`);
      },
      handleCurrentChange(val) {
        console.log(`当前页: ${val}`);
      }
    
    }

}
</script>
<style lang="scss">
 .block{
   text-align: center;
   padding:40px 0;
   background: #fff;
 }
 .block .el-input__inner{
   color:#666;
   margin-left: 0px;
 }
   .el-row {
    margin-bottom: 20px;
    &:last-child {
      margin-bottom: 0;
    }
  }
  .el-col {
    border-radius: 4px;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;

  }
  .alarm_head .el-input{
    width:auto;
    border: 1px solid #ddd
  }

</style>
 