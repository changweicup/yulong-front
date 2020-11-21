<template>
  <div class="login-container">
    <el-form
      class="login-form"
      :model="form"
      ref="registerForm"
      :rules="rules"
      label-width="100px"
      :inline="false"
      size="normal"
    >
      <el-form-item prop="email" label="邮箱">
        <el-input v-model="form.email" placeholder="请输入邮箱"></el-input>
      </el-form-item>
      <el-form-item prop="captcha" label="验证码" class="captcha-container">
        <el-input v-model="form.captcha" placeholder="请输入验证码"></el-input>
        <div class="captcha">
          <img :src="code.captcha" alt="" />
        </div>
      </el-form-item>
      <el-form-item prop="userName" label="昵称">
        <el-input v-model="form.userName" placeholder="请输入昵称"></el-input>
      </el-form-item>
      <el-form-item prop="passwd" label="密码">
        <el-input v-model="form.passwd" placeholder="请输入密码"></el-input>
      </el-form-item>
      <el-form-item prop="repasswd" label="确认密码">
        <el-input
          v-model="form.repasswd"
          placeholder="请再次输入密码"
        ></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click.native.prevent="handleSubmit">注册</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
import md5 from 'md5';

export default {
  layout: 'login',
  methods: {
    resetCaptvcha() {
      this.code.captcha = '/api/captcha?_t' + new Date().getTime(); 
    },
    handleSubmit() {
      this.$refs.registerForm.validate(async valid => {
        if (valid) {
          console.log('校验成功');
          let payload = {
            email: this.form.email,
            userName: this.form.userName,
            passwd: md5(this.form.passwd),
            captcha: this.form.captcha,
          }
          let ret = await this.$http.post('/user/register', payload);
          if (ret.code = 200) {
            this.$alert('注册成功', '成功', {
              confirmButtonText: '去登录',
              callback: ()=> {
                this.$router.push('/login');
              }
            })
          } else {
            this.$message.error(ret.message)
          }
        } else {
          console.log('校验失败')
        }
      })
    }
  },
  data() {
    return {
      form: {
        email: "changweicup@163.com",
        userName: "张长伟",
        passwd: "119728",
        repasswd: "119728",
        captcha: ''
      },
      rules: {
        email: [
          { required: true, message: "请输入邮箱" },
          { type: "email", message: "请输入正确的邮箱格式" },
        ],
        captcha: [
          { required: true, message: "请输入验证码" },
        ],
        userName: [
          { required: true, message: "请输入昵称" },
        ],
        passwd: [
          { required: true, pattern: /^[\w_-]{6, 12}$/g, message: "请输入密码" },
        ],
        repasswd: [
          { required: true, message: "请再次输入密码" },
          {
            validator: (rule, value, callback) => {
              if (value !== this.form.passwd) {
                callback(new Error('两次输入不一致'))
              }
              callback()
            }
          }
        ],
      },
      code: {
        captcha: "/api/captcha",
      },
    };
  },
};
</script>

<style lang="scss" scoped>
</style>