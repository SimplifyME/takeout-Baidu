<template>
  <div class="star-wrap" :class="'star-size-'+size">
    <span v-for="item in scoreClass" :class="item" class="star-item"></span>
  </div>
</template>
<script type="text/ecmascript-6">
  const STAR_NUM = 5
  export default {
    props: {
      score: {
        type: Number,
        validator (value) {
          return value >= 0 && value <= STAR_NUM
        }
      },
      size: {
        type: Number,
        validator (value) {
          return [24, 36, 48].indexOf(value) >= 0
        }
      }
    },
    computed: {
      scoreClass () {
        let star = Math.floor(this.score * 2) / 2
        let intStar = Math.floor(star)
        let halfStar = star % 1 !== 0
        let scoreClass = []

        for (let i = 0; i < intStar; i++) {
          scoreClass.push('star-on')
        }
        halfStar && scoreClass.push('star-half')
        while (scoreClass.length < STAR_NUM) {
          scoreClass.push('star-off')
        }
        return scoreClass
      }
    }
  }
</script>
<style lang="stylus">
  @import "../../common/stylus/mixin.styl"

  .star-wrap
    .star-item
      display: inline-block
      background-size: cover
      background-position: center
    &.star-size-24
      .star-item
        width: 10px
        height: 10px
        margin-right: 3px
        &.last-child
          margin-right: 0
      .star-on
        image-bg('./images/star24_on')
      .star-half
        image-bg('./images/star24_half')
      .star-off
        image-bg('./images/star24_off')
    &.star-size-36
      .star-item
        width: 15px
        height: 15px
        margin-right: 6px
        &.last-child
          margin-right: 0
      .star-on
        image-bg('./images/star36_on')
      .star-half
        image-bg('./images/star36_half')
      .star-off
        image-bg('./images/star36_off')
    &.star-size-48
      .star-item
        width: 20px
        height: 20px
        margin-right: 12px
        &.last-child
          margin-right: 0
      .star-on
        image-bg('./images/star48_on')
      .star-half
        image-bg('./images/star48_half')
      .star-off
        image-bg('./images/star48_off')
</style>
