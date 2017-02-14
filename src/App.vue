<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <router-link class="tab-item" to="/goods">商品</router-link>
      <router-link class="tab-item" to="/ratings">评论</router-link>
      <router-link class="tab-item" to="/seller">商家</router-link>
    </div>
    <router-view></router-view>
  </div>
</template>
<script>
  import header from './components/header/header'

  const RES_OK = 0

  export default{
    data () {
      return {
        seller: {}
      }
    },
    created: function () {
      this.$http.get('/api/seller').then((response) => {
        if (response.body.errno === RES_OK) {
          this.seller = response.body.data
        }
      })
    },
    components: {
      'v-header': header
    }
  }
</script>
<style lang="stylus">
  @import './common/stylus/mixin.styl'
  .tab
    display: flex
    width: 100%
    height: 40px
    line-height: 40px
    // border-bottom: 1px solid rgba(7, 17, 27, 0.1)
    border-bottom-1px(rgba(7, 17, 27, 0.1))
    .tab-item
      flex: 1
      text-align: center
      color: rgb(77, 85, 93)
      font-size: 14px
      &.active
       color: rgb(240, 20, 20)
</style>
