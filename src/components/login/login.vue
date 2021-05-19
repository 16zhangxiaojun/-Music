<template>
  <div class="Loginfroms">
    <el-form
      class="Elfrom"
      :rules="Elfromrules"
      ref="Loginform"
      :model="form"
      label-width="auto"
    >
      <el-form-item class="Input_css" label="账号:" prop="user">
        <el-input
          placeholder="用户名称"
          id="user"
          v-model="form.user"
        ></el-input>
      </el-form-item>
      <el-form-item class="Input_css" label="密码:" prop="pass">
        <el-input
          placeholder="用户密码"
          type="password"
          id="pass"
          v-model="form.pass"
        ></el-input>
      </el-form-item>
      <el-form-item class="button_css">
        <el-button style="margin-right: 1em" @click="Submitlogin"
          >登陆
        </el-button>
        <el-button style="margin-right: 1em">
          <router-link tag="span" class="Linkcss" to="/register"
            >注册</router-link
          >
        </el-button>
        <el-button @click="Restlogin">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  created () {
    this.getUser()
  },
  data () {
    return {
      // 可登录用户
      users: [],
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
    getUser () {
      let usersResult = window.localStorage.getItem('usersList')
      if (usersResult) {
        this.users = JSON.parse(usersResult)
      } else {
        this.users = []
      }
      console.log(this.users)
    },
    Submitlogin () {
      console.log(this.$refs.Loginform.validate())
      this.$refs.Loginform.validate(async (valid) => {
        if (valid) {
          console.log(valid)
          if (this.users.length !== 0) {
            let result = await this.users.some((item) => (item.user === this.form.user && item.pass === this.form.pass))
            if (result) {
              const finduser = this.users.find((item) => item.users === this.form.users)
              window.localStorage.setItem('token', JSON.stringify(finduser.token))
              this.$router.push('/recommend')
            } else {
              alert('不存在此用户!')
            }
          } else {
            alert('暂无用户信息，请注册！')
            this.$router.push('/register')
          }
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    Restlogin () {
      this.$refs.Loginform.resetFields()
    }
  }
}
</script>
<style scoped lang="stylus" rel="stylesheet/stylus">
@import '~common/stylus/variable';

.Loginfroms {
  position: relative;
  box-sizing: border-box;
  width: 100%;
  background-color: #011F3E;
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