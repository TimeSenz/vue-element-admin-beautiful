<template>
  <div class="player-container">
    <el-row :gutter="15">
      <el-col :span="12">
        <el-card shadow="hover">
          <div slot="header">播放传统MP4</div>
          <byui-player-mp4 :config="config1" @player="Player1 = $event" />
        </el-card>
      </el-col>
      <el-col :span="12">
        <el-card shadow="hover">
          <div slot="header">播放m3u8,且不暴露视频地址</div>
          <byui-player-hls :config="config2" @player="Player2 = $event" />
        </el-card>
      </el-col>
      <el-col :span="12">
        <el-card shadow="hover">
          <div slot="header">播放flv,且不暴露视频地址</div>
          <byui-player-flv :config="config3" @player="Player3 = $event" />
        </el-card>
      </el-col>
      <el-col :span="12">
        <el-card shadow="hover">
          <div slot="header">视频大数据专用</div>
          <byui-player-custom
            :config="config4"
            :jump-num="10"
            @getImgSrc="getImgSrc"
            @player="Player4 = $event"
          />
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import {
  byuiPlayerCustom,
  byuiPlayerFlv,
  byuiPlayerHls,
  byuiPlayerMp4,
} from "@/plugins/byuiPlayer.js";

export default {
  name: "Player",
  components: {
    byuiPlayerMp4,
    byuiPlayerHls,
    byuiPlayerFlv,
    byuiPlayerCustom,
  },
  data() {
    return {
      config1: {
        id: "mse1",
        url: "/video/boyun.mp4",
      },
      Player1: null,
      config2: {
        id: "mse2",
        url: "/video/boyun.m3u8",
      },
      Player2: null,
      config3: {
        id: "mse3",
        url: "/video//boyun.flv",
      },
      Player3: null,
      config4: {
        id: "mse4",
        url: "/video/boyun.mp4",
      },
      Player4: null,
    };
  },
  created() {},
  mounted() {},
  methods: {
    getImgSrc(src) {},
  },
};
</script>

<style lang="scss" scoped></style>
