<template>
  <div class="header">
    <div class="left">
      <!-- 界面控制 -->
      <div class="buttons">
        <div class="mac-button red" @click="onClickHome"><Icon :size="9" type="home"/></div>
        <div class="mac-button yellow" @click="exitFullscreen"><Icon :size="9" type="minus"/></div>
        <div class="mac-button green" @click="fullscreen"><Icon :size="9" type="fullscreen"/></div>
      </div>
      <!-- 收起播放页 -->
      <div class="shrink-player" @click="onClickDown">
        <Icon type="down" :backdrop="true"></Icon>
      </div>
      <!-- 路由控制器 -->
      <div class="history">
        <RoutesHistory/>
      </div>
    </div>
    <div class="right">
      <div class="search-wrap">
        <Search/>
      </div>
      <Theme/>
    </div>
  </div>
</template>

<script>
import RoutesHistory from './routes-history.vue'
import Search from './search.vue'
import Theme from './theme.vue'
import { requestFullScreen, exitFullscreen, isFullscreen } from "@/utils";

export default {
  components: { RoutesHistory, Search, Theme },
  methods: {
    onClickHome(){
      this.$router.push('/discovery')
    },
    exitFullscreen(){
      if (isFullscreen()) exitFullscreen()
    },
    fullscreen(){
      requestFullScreen(document.documentElement)
    },
    onClickDown(){
    
    },
  }
}
</script>

<style lang="scss" scoped>
@import "~@/style/element-overwrite.scss";
.header {
  display: flex;
  justify-content: space-between;
  height: $header-height;
  background-color: var(--header-bgcolor);
  padding-right: 36px;

  @include el-input-theme(
    var(--header-input-color),
    var(--header-input-bgcolor),
    var(--header-input-placeholder-color)
  );

  /deep/.iconfont {
    color: var(--header-font-color);
  }

  .left {
    padding: 14px 14px 0 8px;
    display: flex;

    .font-weight {
      white-space: nowrap;
    }

    .buttons {
      display: flex;

      &:hover {
        .mac-button > i {
          opacity: 1;
        }
      }

      .mac-button {
        @include round(14px);
        @include flex-center;
        margin-right: 8px;
        cursor: pointer;

        &.red {
          background: #ed655a;
        }

        &.green {
          background: #72be47;
        }

        &.yellow {
          background: #e0c04c;
        }

        i {
          opacity: 0;
          transform: opacity 0.3s;
          color: $black;
          font-weight: $font-weight-bold;
          transform-origin: center center;
        }
      }
    }

    .shrink-player {
      position: relative;
      top: -6px;
      margin-left: 16px;
    }

    .history {
      margin-left: 65px;
    }
  }

  .right {
    display: flex;
    align-items: center;

    .search-wrap {
      margin-right: 16px;
    }
  }
}
</style>