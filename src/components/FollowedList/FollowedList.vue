<template>
<div class="followed-list">
  <div class="followed-item" v-for="item in list" :key="item.videoInfo.videoId">
    <div class="top">
      <img class="avatar" :src="`${baseURL}${item.userInfo.userAvatar}`" alt="" width="30" height="30"
        @click="chooseUser(item.userInfo.userId)"> <span class="name">@{{item.userInfo.userNickname}}</span>
    </div>
    <div class="desc">{{item.videoInfo.videoDesc}}</div>
    <div class="video-wrap">
      <video class="video"
        :poster="item.videoInfo.videoCover"
        :src="item.videoInfo.videoPath"
        webkit-playsinline
        playsinline
        x5-video-player-type="h5"
        @click.self="playHandler"></video>
    </div>
    <div class="button-bar">
      <div class="like iconfont icon-heart-fill" :class="{ 'red-heart': like }" @click="toggleLike">
        <span class="likenum">{{item.WSLCNum.likeNum}}</span>
      </div>
      <div class="comment iconfont icon-message" @click.stop="showCommentList(item.videoInfo.videoId, item.WSLCNum.commentNum)">
        <span class="commentnum">{{item.WSLCNum.commentNum}}</span>
      </div>
      <div class="share iconfont icon-share">
        <span class="sharenum">{{item.WSLCNum.shareNum}}</span>
      </div>
    </div>
    <div class="time">{{formatTime(item.videoInfo.createdAt)}}</div>
  </div>
  <no-more class="no-more"></no-more>
</div>
</template>

<script>
import NoMore from 'base/NoMore/NoMore'
import { baseURL } from 'common/js/config'
import { formatTime } from 'common/js/util'
export default {
  props: {
    list: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      like: false,
      baseURL
    }
  },
  methods: {
    showCommentList (videoId, commentNum) {
      this.$emit('showCommentList', videoId, commentNum)
    },
    playHandler (e) {
      const v = e.target
      v.paused ? v.play() : v.pause()
    },
    toggleLike () {
      this.like = !this.like
    },
    chooseUser (userId) {
      if (this.$route.path === '/followed') {
        this.$router.push(`/profile/${userId}`)
      }
    },
    formatTime
  },
  components: {
    NoMore
  }
}
</script>

<style scoped lang='stylus'>
@import '~@/common/stylus/variable'
.followed-list
  margin 10px 10px 0 10px
  .no-more
    margin-top 12px
  .followed-item
    margin-top 10px
    display flex
    flex-direction column
    border-bottom 1px solid $color-divide
    &:nth-last-child(2)
      border none
    .top
      .name
        color $color-white
        margin-left 5px
        vertical-align top
        line-height 32px
        font-size $font-size-medium
      .avatar
        border-radius 50%
    .desc
      font-size $font-size-medium
      margin 10px 0
      color $color-text
    .video-wrap
      position relative
      width 70%
      height 400px
      .video
        display block
        object-fit cover
        width 100%
        height 100%
        border-radius 5px
    .button-bar
      margin 10px 0
      display flex
      width 50%
      justify-content space-between
      .like
        position relative
        .likenum
          font-size $font-size-small-s
          position absolute
          left 100%
          top 50%
          transform translateX(20%) translateY(-50%)
          color $color-text
      .red-heart
        color rgb(248, 53, 95)
      .comment
        position relative
        .commentnum
          font-size $font-size-small-s
          position absolute
          left 100%
          top 50%
          transform translateX(20%) translateY(-50%)
      .share
        position relative
        .sharenum
          font-size $font-size-small-s
          position absolute
          left 100%
          top 50%
          transform translateX(20%) translateY(-50%)
    .button-bar > div
      width 26px
      height 26px
      font-size 26px
      color $color-btn
      transition color .3s
    .time
      margin-bottom 20px
      color $color-desc
      font-size $font-size-small-s
</style>
