<template>
  <div class="conter">
    <el-card class="box-card">
      <div class="login_title">
        <img src="../../assets/logo.png">
      </div>
      <el-form :model="ruleForm"
               :rules="loginRules"
               ref="formData">
        <el-form-item prop="mobile">
          <el-input placeholder="请输入手机号"
                    v-model="ruleForm.mobile"></el-input>
        </el-form-item>
        <el-form-item prop="code">
          <el-input placeholder="请输入验证码"
                    class="input-code"
                    v-model="ruleForm.code"></el-input>
          <el-button class="btns">验证码</el-button>
        </el-form-item>
        <el-form-item class="check-info">
          <el-checkbox label="我已阅读并同意用户协议和隐私条款"
                       v-model="ruleForm.check"></el-checkbox>
        </el-form-item>
        <el-form-item>
          <el-button type="primary"
                     @click="getLogin">登陆</el-button>
        </el-form-item>
      </el-form>
    </el-card>

    <Vcode :show="isShow"
           :sliderText='sliderText'
           :canvasWidth='canvasWidth'
           @onSuccess="onSuccess"
           @onClose="onClose"
           id="rand-info" />
  </div>
</template>

<script>
import Vcode from 'vue-puzzle-vcode'
// import Img1 from '../../assets/1.jpg'
// import Img2 from '../../assets/2.jpg'
export default {
  name: 'login',
  data () {
    return {
      isShow: false,
      canvasWidth: 210,
      // canvasHeight: 80,
      sliderText: '再加油一点',
      // Img1,
      // Img2,
      loading: true,
      ruleForm: {
        mobile: '',
        code: '',
        check: 'false'
      },
      loginRules: {
        mobile: [{ required: true, message: '请输入您的手机号' }, {
          pattern: /^1[3456789]\d{9}$/, message: '手机号格式不正确'
        }],
        code: [{ required: true, message: '请输入您的验证码' }, {
          pattern: /^\d{6}$/,
          message: '验证码格式不正确'
        }],
        check: [{ validator: function (rule, value, callback) {
          if (value) {
            callback()
          } else {
            callback(new Error('您必须无条件同意被我们坑'))
          }
        } }]
      }
    }
  },
  components: {
    Vcode
  },
  methods: {
    onSubmit () {
      this.isShow = true
    },
    onSuccess (msg) {
      this.isShow = false // 通过验证后，需要手动隐藏模态框
    },
    // 用户点击遮罩层，应该关闭模态框
    onClose () {
      this.isShow = false
    },
    getLogin () {
      // console.log(this.$refs.formData)
      this.$refs.formData.validate((isOk) => {
        if (isOk) {
          this.onSubmit()
        }
      })
    }
  },
  created () {
    // this.onSubmit()
  }
}
</script>

<style lang='less' scoped>
.conter {
  height: 100vh;
  background-image: url("../../assets/login_bg.jpg");
  background-size: cover;
  display: flex;
  justify-content: center;
  align-items: center;
  /deep/ .el-card__body {
    padding: 0;
  }
  .box-card {
    width: 400px;
    height: 300px;
    padding: 20px;

    .login_title {
      margin-bottom: 20px;
      text-align: center;
      img {
        height: 44px;
      }
    }
    .input-code {
      width: 65%;
    }
    .btns {
      width: 30%;
      margin-left: 10px;
    }
    .check-info {
      text-align: left;
    }
  }
}
.el-button--primary {
  width: 100%;
}
#rand-info {
  /deep/ .vue-auth-box {
    padding: 10px;
  }
  /deep/ .range-box {
    height: 8px;
  }
  /deep/ .range-btn {
    height: 8px;
  }
}
</style>
