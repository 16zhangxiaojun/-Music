<template>
  <div id="app">
    <m-header v-if="Urlflag"></m-header>
    <tab v-if="Urlflag"></tab>
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
    <player v-if="Urlflag"></player>
  </div>
</template>

<script type="text/ecmascript-6">
import mHeader from '@/components/m-header/m-header.vue'
import tab from '@/components/tab/tab.vue'
import player from '@/components/player/player.vue'
export default {
  beforeUpdate () {
    this.Url()
  },
  data () {
    return {
      Urlflag: ''
    }
  },
  components: {
    mHeader,
    tab,
    player
  },
  methods: {
    Url () {
      const tempUrl = this.$route.path
      if (tempUrl === '/login' || tempUrl === '/register') {
        this.Urlflag = false
      } else {
        this.Urlflag = true
      }
      console.log(this.$route.path)
    }
  }
}
</script>

<style scoped lang="stylus" rel="stylesheet/stylus"></style>
