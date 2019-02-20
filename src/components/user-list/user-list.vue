<template>
   <div>
     <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>用户管理</el-breadcrumb-item>
      <el-breadcrumb-item>用户列表</el-breadcrumb-item>
    </el-breadcrumb>
    <el-row class="search-wrap">
      <el-col :span="8">
        <el-input placeholder="请输入内容" v-model="searching" class="input-with-select">
          <el-button slot="append" icon="el-icon-search"></el-button>
        </el-input>
      </el-col>
      <el-col :span="4"><el-button type="success" plain>添加用户</el-button></el-col>
    </el-row>
    <el-table
      :data="tableData"
      style="width: 100%">
      <el-table-column
        prop="username"
        label="姓名"
        width="280">
      </el-table-column>
      <el-table-column
        prop="email"
        label="邮箱"
        width="280">
      </el-table-column>
      <el-table-column
        prop="mobile"
        label="电话"
        width="280">
      </el-table-column>
      <el-table-column
        prop=""
        label="操作">
      </el-table-column>
    </el-table>
    <el-pagination
      class="page-set"
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage4"
      :page-sizes="[100, 200, 300, 400]"
      :page-size="100"
      layout="total, sizes, prev, pager, next, jumper"
      :total="400">
    </el-pagination>
   </div>
</template>
<script>
import axios from 'axios'
export default {
  async created () {
    const data=JSON.parse(window.localStorage.getItem('admin-token'))
    const token=data.data.token
    const res=await axios.get('http://localhost:8888/api/private/v1/users',{
      headers:{
        Authorization:token
      },
      params:{
        pagenum:1,
        pagesize:5
      }
    })
    console.log(res);
    this.tableData=res.data.data.users
  },
  data () {
    return {
      tableData: [],
      currentPage1: 5,
      currentPage2: 5,
      currentPage3: 5,
      currentPage4: 4,
      searching:""
    }
  },
  methods: {
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
    }
  }
}
</script>
<style>
.search-wrap,.page-set{
  margin: 15px 0;
}
</style>
