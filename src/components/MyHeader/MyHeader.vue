<template>
  <div class="my-header">
    <div class="back-wrap" v-if="hasBack">
      <span class="iconfont icon-left" @click="GoBack"></span>
    </div>
    <div>
      <span>
        {{title}}
      </span>
    </div>
    <div class="contact-wrap" v-if="title == '消息'" @click="$router.push('/contact')">
      <span>联系人</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    hasBack: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    GoBack () {
      this.$router.back()
    }
  }
}
</script>

<style scoped lang='stylus'>
@import '~@/common/stylus/variable'
.my-header
  display flex
  position relative
  justify-content center
  color $color-text
  height 44px
  line-height 44px
  font-size $font-size-medium-x
  z-index 33
  .back-wrap
    position absolute
    left: 10px
  .contact-wrap
    position absolute
    right 10px
</style>
