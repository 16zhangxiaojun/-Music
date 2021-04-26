/* eslint-disable no-unused-expressions */
<template>
  <div class="Registerfroms">
    <el-form
      class="Elfrom"
      :rules="Elfromrules"
      ref="Registerform"
      :model="form"
      label-width="auto"
    >
      <el-form-item class="Input_css" label="注册账号:" prop="user">
        <el-input
          placeholder="用户名称"
          id="user"
          v-model="form.user"
        ></el-input>
      </el-form-item>
      <el-form-item class="Input_css" label="注册密码:" prop="pass">
        <el-input
          placeholder="用户密码"
          type="password"
          id="pass"
          v-model="form.pass"
        ></el-input>
      </el-form-item>
      <el-form-item class="button_css">
        <el-button style="margin-right: 1em">
          <router-link
            tag="span"
            class="Linkcss"
            to="/login"
            @click.native="refresh"
            >登陆</router-link
          >
        </el-button>
        <el-button style="margin-right: 1em" @click="Register_now">
          立即注册
        </el-button>
        <el-button @click="Restlogin">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  data () {
    return {
      str: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'],
      users: [], // 可登录用户
      compareArry: [], // 临时存储用户数组
      form: {
        user: '',
        pass: ''
      },
      Elfromrules: {
        user: [
          { required: true, message: '请输入用户', trigger: 'blur' },
          { min: 1, max: 10, message: '长度在 1 到 10 个字符', trigger: 'blur' }
        ],
        pass: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 5, max: 9, message: '长度在 5 到 9 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    generateMixed (n) {
      var res = ''
      for (var i = 0; i < n; i++) {
        var id = Math.ceil(Math.random() * 35)
        res += this.str[id]
      }
    //   console.log(res)
      return res
    },
    Register_now () {
      console.log(this.form)
      this.$refs.Registerform.validate(async (valid) => {
        if (valid) {
          console.log(valid)
          if (this.users.length !== 0) {
            console.log('valid')
            this.compareArry = [...this.users]
            let checkValue = await this.compareArry.some((item) => { return item.user === this.form.user })
            if (checkValue) {
              alert('用户名重复！')
              return false
            } else {
              this.checkRepeat()
            }
            console.log(this.users)
          } else {
            this.checkRepeat()
          }
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    checkRepeat () {
      this.users.push({
        user: this.form.user,
        pass: this.form.pass,
        token: this.generateMixed(12)
      })
      let sessionUers = this.users
      window.sessionStorage.setItem('usersList', JSON.stringify(sessionUers))
      console.log(this.users)
      alert('注册成功！')
    },
    Restlogin () {
      this.$refs.Registerform.resetFields()
    },
    refresh () {
      this.$router.go(0)
    }
  }
}
</script>
<style scoped lang="stylus" rel="stylesheet/stylus">
@import '~common/stylus/variable';

.Registerfroms {
  position: relative;
  box-sizing: border-box;
  width: 100%;
  background-color: #23A7F2;
  padding: 1em;
  top: 50%;
  transform: translate(0, 100%);
  box-shadow: 2px 2px 5px #888888;

  .Elfrom {
    box-sizing: border-box;
    padding: 1em;

    .Input_css {
      display: flex;
      justify-content: space-around;
      align-items: center;
      padding: 1em;
    }

    .button_css {
      display: flex;
      justify-content: flex-end;
      align-items: center;
      margin-right: 2em;

      .Linkcss {
        color: #000000;
      }
    }
  }
}
</style>