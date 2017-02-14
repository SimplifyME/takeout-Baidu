<template>
  <div class="shop-header">
    <div class="header-content">
      <img class="shop-logo" :src="seller.avatar">
      <div class="shop-info">
        <p class="shop-name-wrap">
          <span class="shop-auth" v-if="seller.is_premium"></span>
          <span class="shop-name">{{seller.name}}</span>
        </p>
        <p class="shop-delivery">{{seller.description}} / {{seller.deliveryTime}}送达</p>
        <p class="shop-activity" v-if="seller.supports">
          <span class="activity-icon" :class="activityIcon"></span>
          <span class="activity-description">{{seller.supports[0].description}}</span>
            <span class="activity-count-warp" v-if="seller.supports" @click="showDetail">
                {{seller.supports.length}}个活动
                <i class="icon icon-keyboard_arrow_right"></i>
            </span>
        </p>
      </div>
    </div>
    <!--公告-->
    <div class="header-bulletin" @click="showDetail">
      <span class="tip"></span>
      {{seller.bulletin}}
      <i class="icon icon-keyboard_arrow_right"></i>
    </div>
    <!--背景-->
    <div class="shop-background image-bg" :style="{backgroundImage: 'url('+seller.avatar+')'}"></div>
    <!--公告详情-->
    <transition name="fade">
      <div class="detail" v-show="detailShow" transition="fade">
        <div class="detail-content">
          <h1>{{seller.name}}</h1>
          <star :size="48" :score="seller.score" class="star"></star>
          <div class="title">
            <div class="line"></div>
            <div class="text">优惠信息</div>
            <div class="line"></div>
          </div>
          <ul class="activity">
            <li v-for="item in seller.supports">
              <span :class="activityMap[item.type]" class="activity-icon"></span>
              <span class="description">{{item.description}}</span>
            </li>
          </ul>
          <div class="title">
            <div class="line"></div>
            <div class="text">商家公告</div>
            <div class="line"></div>
          </div>
          <p class="bulletin">{{seller.bulletin}}</p>
        </div>
        <div class="close"><i class="icon-close" @click="closeDetail"></i></div>
      </div>
    </transition>

  </div>
</template>
<script type="text/ecmascript-6">
  import star from 'components/star/star'

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data () {
      return {
        activityMap: ['decrease', 'discount', 'guarantee', 'invoice', 'special'],
        detailShow: false
      }
    },
    computed: {
      // 活动类型转换为对应图标
      activityIcon () {
        if (this.seller.supports && this.seller.supports[0]) {
          return this.activityMap[this.seller.supports[0].type]
        } else {
          return ''
        }
      }
    },
    components: {
      star
    },
    methods: {
      showDetail () {
        this.detailShow = true
      },
      closeDetail () {
        this.detailShow = false
      }
    }
  }
</script>
<style lang="stylus">
  @import "../../common/stylus/mixin.styl"

  .shop-header
    position: relative
    background-color: rgba(7, 17, 27, 0.5)
    overflow: hidden
    .header-content
      padding: 24px 12px 18px 24px
      color: #FFFFFF
      font-size: 0
      font-weight: 200
      .shop-logo
        display: inline-block
        vertical-align: top
        border-radius: 2px
        width: 64px
        height: 64px
      .shop-info
        display: inline-block
        font-size: 12px
        padding: 2px 0 2px 16px
        width: calc(100% - 64px)
        box-sizing: border-box
        .shop-name-wrap, .shop-name, .shop-delivery, .shop-activity
          overflow: hidden
          white-space: nowrap
          text-overflow: ellipsis
        .shop-name-wrap
          font-size: 0
          .shop-auth
            display: inline-block
            vertical-align: top
            width: 30px
            height: 18px
            image-bg('./images/brand')
          .shop-name
            font-size: 16px
            line-height: 18px
            font-weight: bold
            margin-left: 6px
        .shop-delivery
          font-size: 12px
          line-heght: 12px
          margin-top: 8px
        .shop-activity
          position: relative
          font-size: 10px
          line-height: 18px
          margin-top: 6px
          padding-right: 75px
          .activity-icon
            display: inline-block
            vertical-align: middle
            width: 12px
            height: 12px
            &.decrease
              image-bg('./images/decrease_1')
            &.discount
              image-bg('./images/discount_1')
            &.guarantee
              image-bg('./images/guarantee_1')
            &.invoice
              image-bg('./images/invoice_1')
            &.special
              image-bg('./images/special_1')
          .activity-count-warp
            display: inline-block
            position: absolute
            right: 0px
            bottom: 0px
            font-size: 10px
            line-height: 18px
            height: 18px
            background-color: rgba(0, 0, 0, .2)
            border-radius: 14px
            padding: 0px 14px 0 8px
            text-align: center
            .icon
              position: absolute
              top: 0
              right: 3px
              line-height: 18px
    .header-bulletin
      position: relative
      overflow: hidden
      white-space: nowrap
      text-overflow: ellipsis
      color: white
      background-color: rgba(7, 17, 27, 0.2)
      font-size: 10px
      font-weight: 200
      height: 28px
      line-height: 28px
      padding: 0 12px
      .tip
        display: inline-block
        width: 22px
        height: 12px
        image-bg('./images/bulletin')
        vertical-align: middle
      .icon
        position: absolute
        right: 10px
        bottom: 0
        line-height: inherit;
    .shop-background
      position: absolute
      left: 0
      top: 0
      width: 100%
      height: 100%
      z-index: -1
      filter: blur(10px)
    .detail
      position: fixed
      left: 0
      top: 0
      width: 100%
      height: 100%
      padding: 0 36px 96px
      background-color: rgba(7, 17, 27, 0.9)
      z-index: 100
      overflow: hidden
      .detail-content
        color: #FFFFFF
        overflow: auto
        height: 100%
        h1
          font-size: 16px
          font-weight: 700
          line-height: 16px
          text-align: center
          margin-top: 64px
        .star
          text-align: center
          margin-top: 16px
        .title
          display: flex
          font-size: 14px
          font-weight: 800
          line-height: 14px
          width: 100%
          margin: 28px auto 0
          .line
            flex: 1
            border-top: 1px solid rgba(255, 255, 255, 0.2)
            margin-top: 7px
          .text
            padding: 0 24px
        .activity
          width: 100%
          margin: 24px auto 0
          font-size: 12px
          li
            margin-top: 6px
            .activity-icon
              display: inline-block
              width: 16px
              height: 16px
              &.decrease
                image-bg('./images/decrease_2')
              &.discount
                image-bg('./images/discount_2')
              &.guarantee
                image-bg('./images/guarantee_2')
              &.invoice
                image-bg('./images/invoice_2')
              &.special
                image-bg('./images/special_2')
            .description
              display: inline-block
              vertical-align: top
              line-height: 16px
        .bulletin
          margin-top: 24px
          font-size: 12px
          line-height: 24px
      .close
        position: absolute
        bottom: 32px
        left: 0
        text-align: center
        width: 100%
        color: rgba(255, 255, 255, 0.5)
        font-size: 32px

</style>
