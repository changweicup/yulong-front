<template>
  <nuxt/>
</template>

<script>
export default {

}
</script>

<style lang="scss">
  .login-container {
    width: 100%;
    min-height: 100%;
    .login-form {
      width: 520px;
      padding: 160px 0;
      margin: 0 auto;
      overflow: hidden;
      .captcha-container{
        width:80%;
        position: relative;
        .captcha {
          position: absolute;
          right: -110px;
          top: -6px;
          img {
            width: 90px;
            height: 50px;
            cursor: pointer;
          }
        }
      }
    }
  }
</style>