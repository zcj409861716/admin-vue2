<template>
  <el-container class="home-wrap">
    <el-header class="home-header">
      <el-row>
        <el-col :span="5"><div class="grid-content bg-purple"><img src="../../assets/logo.png" alt=""></div></el-col>
        <el-col :span="4" :offset="15">
          <div class="grid-content bg-purple-light">
            <el-button
              class="home-logout"
              @click="logout"
              type="text">退出登录</el-button>
          </div>
        </el-col>
      </el-row>
    </el-header>
    <!--侧边栏-->
    <el-container class="home-main">
      <el-aside class="home-aside" width="200px">
        <el-menu
          default-active="2"
          class="el-menu-vertical-demo home-aside-list"
          @open="handleOpen"
          @close="handleClose"
          :unique-opened="true"
          :router="true"
          background-color="#545c64"
          text-color="#fff"
          active-text-color="#ffd04b">

          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>用户管理</span>
            </template>
            <el-menu-item index="/users">用户列表</el-menu-item>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>权限管理</span>
            </template>
            <el-menu-item index="/roles">角色列表</el-menu-item>
            <el-menu-item index="2-2">权限列表</el-menu-item>
          </el-submenu>
          <el-submenu index="3">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>商品管理</span>
            </template>
            <el-menu-item index="3-1">商品列表</el-menu-item>
            <el-menu-item index="3-2">商品分类</el-menu-item>
            <el-menu-item index="3-3">商品参数</el-menu-item>
          </el-submenu>
          <el-submenu index="4">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>订单管理</span>
            </template>
            <el-menu-item index="4-1">订单列表</el-menu-item>
          </el-submenu>
          <el-submenu index="5">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>数据统计</span>
            </template>
            <el-menu-item index="5-1">数据报表</el-menu-item>
          </el-submenu>


        </el-menu>
      </el-aside>
      <el-main class="home-main" >
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>
<script>
export default {
  data () {
    return {

    }
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
    logout() {
      this.$confirm('是否确定退出登录?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        window.localStorage.removeItem('admin-token')
        this.$router.push({
          name:'login'
        })
        this.$message({
          type: 'success',
          message: '退出成功!'
        });
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消退出'
        });
      });
    }
  }
}
</script>
<style>
.home-wrap,.home-main,.home-aside,.home-aside-list{
  height: 100%;
}
.home-header{
  background-color:gray;
}
.home-main{
  background-color:rgb(223, 214, 214);
}
.home-logout{
  margin-top: 10px;
}
</style>
