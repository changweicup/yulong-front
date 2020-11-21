<template>
  <div>
    <el-form class="login-form">
      <el-form-item label="邮箱" prop="email">
        <i class="el-icon-email"></i>
        <el-input v-model="form.email"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="passwd">
        <i class="el-icon-lock"></i>
        <el-input type="password" v-model="form.passwd"></el-input>
      </el-form-item>
      <el-form-item label="验证码" prop="captcha">
        <img @click="updataCaptcha" :src="captchaUrl" alt="">
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  layout: 'login',
  data() {
    return {
      form: {
        email: 'changweicup@163.com',
        passwd: 'admin'
      },
      captchaUrl: '/api/captcha?_t='+ new Date().getTime()
    }
  },
  methods: {
    updataCaptcha() {
      this.captchaUrl = '/api/captcha?_t='+ new Date().getTime();
    }
  }
};
</script>

<style>
</style>