<!-- Please remove this file from your project -->
<template>
  <div>
    <client-only>
      <video-player
        ref="videoPlayer"
        :options="playerOptions"
        @play="onPlayerPlay($event)"
        @ready="onPlayerReady($event)"
      />
    </client-only>
  </div>
</template>

<script>
import { defineComponent } from "@vue/composition-api";

export default defineComponent({
  name: "Video",
  setup() {},
  publicRuntimeConfig: {
    baseURL: process.env.BASE_URL || '127.0.0.1:33001'
  },
  data() {
    return {
      src: `http://${this.$config.baseURL}/camera/livestream.m3u8`,
      playerOptions: {
        autoplay: true,
        controls: true,
        controlBar: {
          timeDivider: false,
          durationDisplay: false
        },
        autoplay: "true",
        muted: "muted",
      }
    };
  },
  computed: {
    player() {
      return this.$refs.videoPlayer.player;
    }
  },
  methods: {
    onPlayerPlay(player) {},
    onPlayerReady(player) {},
    playVideo: function(source) {
      const player = this.$refs.videoPlayer.player;
      const video = {
        withCredentials: false,
        type: "application/x-mpegurl",
        src: source
      };
      player.reset(); // in IE11 (mode IE10) direct usage of src() when <src> is already set, generated errors,
      player.src(video);
      // this.player.load()
      player.play();
    },
    switchPlayer: function() {
      this.playVideo(this.src);
    }
  },
  mounted() {
    setTimeout(() => {
      this.playVideo(this.src);
    }, 500);
  }
});
</script>
