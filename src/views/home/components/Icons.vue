<template>
  <div class="icons">
    <swiper :options="swiperOption">
      <swiper-slide class="page" v-for="(page, index) of pages" :key="index">
        <div class="icon" v-for="item of page" :key="item.id">
          <div class="icon-img">
            <img class="icon-img-content" :src="item.imgUrl" alt="icon">
          </div>
          <p class="icon-title">{{item.title}}</p>
        </div>
      </swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeIcons',
  props: {
    list: Array
  },
  data() {
    return {
      swiperOption: {
        pagination: {
          el: '.swiper-pagination'
        },
        autoplay: false
      }
    }
  },
  computed: {
    pages() {
      const pages = []
      this.list.forEach((item, index) => {
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/variable.styl'
@import '~styles/mixins.styl'
.icons
  background #fff
  position relative
  overflow hidden
  height 0
  padding-bottom 54%
  .page
    margin-bottom 0.26rem
    .icon
      border none
      position relative
      overflow hidden
      float left
      width 25%
      padding-bottom 25%
      height 0
      .icon-img
        position absolute
        top 0
        right 0
        bottom 0.44rem
        left 0
        box-sizing border-box
        padding 0.1rem
        .icon-img-content
          display block
          margin 0 auto
          height 100%
      .icon-title
        display block
        position absolute
        text-align center
        bottom 0
        left 0
        right 0
        height 0.44rem
        line-height 0.44rem
        color $normalTextColor
        @include ellipsis .swiper-pagination position absolute bottom 0
</style>