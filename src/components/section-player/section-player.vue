<template>
  <div class="section-player">
    <!--@play="onPlayerPlay($event)"-->
    <!--@pause="onPlayerPause($event)"-->
    <video-player class="video-player vjs-custom-skin" ref="videoPlayer" :playsinline="true" :options="playerOptions">
    </video-player>

  </div>
</template>

<script>
  export default {
    name: "section-player",
    props: {
      videoUrl: String,
      state: Boolean
    },
    data() {
      return {
        playerOptions: {
          // playbackRates: [0.7, 1.0, 1.5, 2.0], //播放速度
          autoplay: false, // 如果true,浏览器准备好时开始回放。
          muted: false, // 默认情况下将会消除任何音频。
          loop: false, // 导致视频一结束就重新开始。
          preload: 'auto', // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
          language: 'zh-CN',
          aspectRatio: '16:9', // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
          fluid: true, // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
          sources: [{
            type: 'video/mp4',
            src: this.videoUrl// 你的m3u8地址（必填）
          }],
          // poster: 'https://surmon-china.github.io/vue-quill-editor/static/images/surmon-3.jpg', // 你的封面地址
          width: document.documentElement.clientWidth,
          // heigth:document.documentElement.clientHeight,
          notSupportedMessage: '此视频暂无法播放，请稍后再试',// 允许覆盖Video.js无法播放媒体源时显示的默认信息。
          // isFullscreen: true,
        }
      }
    },
    watch: {
      //更改视频源 videoUrl从弹出框组件传值
      videoUrl(val) {
        if (val !== '') {
          // this.$refs.videoPlayer.player.src(val)
          this.player.src(val);
        }
      },
      state(val) {
        if (val) {
          // this.$refs.videoPlayer.player.pause()
          this.player.pause()
        }else{
          // this.$refs.videoPlayer.player.currentTime(0);
          // this.$refs.videoPlayer.player.play()
          this.player.currentTime(0);
          this.player.play();
        }
      }
    },
    methods: {
      // onPlayerPlay (player) {
      //   console.log("播放",player);
      // },
      // onPlayerPause (player) {
      //   console.log("暂停",player);
      // },
      // playerStateChanged (player) {
      //   console.log("播放状态发生改变",player);
      // },
    },
    computed: {
      player () {
        return this.$refs.videoPlayer.player
      }
    },
  }
</script>

<style>
  /*@import '../../../../node_modules/video.js/dist/video-js.css';*/
  /*@import '../../../../node_modules/vue-video-player/src/custom-theme.css';*/
  .video-js .vjs-big-play-button[title="Play Video"] {
    position: absolute;
    left: 50% !important;
    top: 50% !important;
    transform: translate(-50%,-50%) !important;
  }

</style>
