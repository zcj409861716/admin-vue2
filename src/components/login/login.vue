<template>
   <div class='login-wrap'>
     <el-form label-position="top" class="login-form"  ref="form" :model="userForm" label-width="80px">
      <el-form-item label="用户名">
        <el-input
          v-model="userForm.username"></el-input>
      </el-form-item>
      <el-form-item label="密码">
        <el-input
          type='password'
          v-model="userForm.password"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button class='login-btn' type="primary" @click="login">登录</el-button>
      </el-form-item>
    </el-form>
   </div>
</template>
<script>
import axios from 'axios'
export default {
  data () {
    return {
      userForm:{
        username:'',
        password:''
      }
    }
  },
  methods: {
   async login () {
     const res=await axios.post('http://localhost:8888/api/private/v1/login',this.userForm)
     const data=res.data
     if(data.meta.status===200){
       window.localStorage.setItem('admin-token',JSON.stringify(data))
       this.$router.push({
         name:'home'
       })

     }
   }
  }
}
</script>
<style>
.login-wrap{
  background-color: #B3C0D1;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center
}
.login-form{
  background-color: #fff;
  width:400px;
  padding: 50px;
  border-radius: 10px;
}
.login-btn{
  width: 100%;
}

</style>
