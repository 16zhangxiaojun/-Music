<template>
  <div class="m-header">
    <span class="signout" @click="signOut">退出</span>
    <div class="icon"></div>
    <h1 class="text">听点-Music</h1>
    <router-link tag="div" class="mine" to="/user">
      <i class="icon-mine"></i>
    </router-link>
  </div>
</template>

<script type="text/ecmascript-6">
export default {

  methods: {
    signOut () {
      // window.localStorage.clear('token') 清除全部存储数据
      window.localStorage.removeItem('token') // 清除指定数据
      this.$router.push('/login')
    }
  }
}
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
@import '~common/stylus/variable';
@import '~common/stylus/mixin';

.m-header {
  position: relative;
  height: 44px;
  text-align: center;
  color: $color-theme;
  font-size: 0;

  .signout {
    height: 30px;
    width: auto;
    vertical-align: top;
    position: absolute;
    top: 5px;
    left: 0;
    line-height: 30px;
    font-size: $font-size-large;
    margin-left: 5px;
  }

  .icon {
    display: inline-block;
    vertical-align: top;
    margin-top: 6px;
    width: 30px;
    height: 30px;
    margin-right: 9px;
    bg-image('A0000028');
    background-size: 30px 30px;
    border-radius: 15px;
    background-repeat: no-repeat;
  }

  .text {
    display: inline-block;
    vertical-align: top;
    line-height: 44px;
    font-size: $font-size-large;
  }

  .mine {
    position: absolute;
    top: 0;
    right: 0;

    .icon-mine {
      display: block;
      padding: 12px;
      font-size: 20px;
      color: $color-theme;
    }
  }
}
</style>