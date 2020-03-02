<template>
  <el-row type="flex" align="middle" justify="center">
    <el-col :span="8">
      <el-form
        :model="loginForm"
        :rules="rules"
        ref="loginForm"
        class="demo-ruleForm"
      >
        <el-form-item label="用户名" prop="username">
          <el-input v-model="loginForm.username"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="password">
          <el-input v-model="loginForm.password"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="startLogin">登录</el-button>
          <el-button @click="reset">重置</el-button>
        </el-form-item>
      </el-form>
    </el-col>
  </el-row>
</template>
<script>
import axios from 'axios'
export default {
  data () {
    return {
      loginForm: {
        username: 'admin',
        password: '123456'
      },
      rules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在3-10个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    startLogin () {
      console.log(this.$refs.loginForm)
      this.$refs.loginForm.validate(valid => {
        console.log('mm' + valid)
        if (!valid) {
          this.$message({
            message: '请输入正确的用户名和密码',
            type: 'warning',
            showClose: true,
            duration: 1000
          })
        }

        axios
          .post('http://localhost:8888/api/private/v1/login', this.loginForm)
          .then(res => {
            console.log('res', res)
            if (res.data.meta.status === 200) {
              this.$message({
                message: '登录成功',
                type: 'success',
                duration: 1000
              })

              // 跳转到首页
              this.$router.push('./home')
            }
          })
      })
    },
    reset () {
      this.$refs.loginForm.resetFields()
    }
    //   submitForm(formName) {
    //     this.$refs[formName].validate(valid => {
    //       if (valid) {
    //         alert("submit!");
    //       } else {
    //         console.log("error submit!!");
    //         return false;
    //       }
    //     });
    //   },
    //   resetForm(formName) {
    //     this.$refs[formName].resetFields();
    //   }
  }
}
</script>
<style scoped>
.el-row {
  height: 100%;
  background-color: darkgreen;
}
.el-form {
  padding: 40px 20px;
  background-color: #fff;
  border-radius: 30px;
}
</style>
