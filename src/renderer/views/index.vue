<template>
  <div class="bear">
    <div class="bear-header">
      <div class="bear-header-title">Drag</div>
      <div class="bear-header-btngroup">
        <!-- <Icon
          class="bear-header-btngroup-handle"
          :size="22"
          type="ios-remove"
          @click="changeWinMin()"
        />
        <Icon
          class="bear-header-btngroup-handle"
          :size="16"
          type="ios-browsers-outline"
          v-if="maxState"
          @click="changeWinMax(false)"
        />

        <Icon
          class="bear-header-btngroup-handle"
          :size="16"
          type="ios-square-outline"
          v-else
          @click="changeWinMax(true)"
        />-->
        <i class="el-icon-ice-cream-round" v-if="maxState" @click="changeWinMax(false)"></i>
        <i class="el-icon-ice-cream-square" v-else @click="changeWinMax(true)"></i>
        <i class="el-icon-close" @click="changeWinClose()"></i>
        <!-- <Button @click="changeWinHide(true)">显示</Button>
        <Button @click="changeWinHide(false)">隐藏</Button>-->
        <!-- <Icon
          class="bear-header-btngroup-handle"
          :size="24"
          type="ios-close"
          @click="changeWinClose()"
        />-->
      </div>
    </div>
    <div class="bear-content">
      <div class="bear-content-left">
        <div v-for="(item,key) in routerRes" :key="key" @click="onRouterPush(item.path)">
          <span>{{item.name}}</span>
        </div>
        <!-- <Button @click="changeWinDirect(true)">窗口大</Button>
        <Button @click="changeWinDirect(false)">窗口小</Button>-->
        <el-button type="primary" icon="el-icon-search">搜索</el-button>
      </div>
      <div class="bear-content-wrapper">
        <router-view></router-view>
      </div>
    </div>
    <div class="bear-footer">
      <span class="bear-footer-version">BearACGWin @verson 0.0.1</span>
      <span class="bear-footer-copyright">
        <!-- Copyright © 2019 - 2119 JuvoS. All Rights Reserved.JuvoS / License MIT -->
        Copyright © 2019 ACG All Rights Reserved.
      </span>
    </div>
  </div>
</template>

<script>
import { appRouter } from "../router/defines";
// import WindowUtil from "../common/WindowUtil";
import { ipcRenderer } from "electron";
import { fail } from "assert";
export default {
  data() {
    return {
      maxState: false
    };
  },
  computed: {
    routerRes() {
      return appRouter.children;
    }
  },
  mounted() {},
  methods: {
    onRouterPush(v) {
      this.$router.push("/" + v);
    },
    changeWinMin() {
      ipcRenderer.send("min");
    },

    changeWinMax(v) {
      this.maxState = v;
      if (v) return ipcRenderer.send("max");
      return ipcRenderer.send("unmax");
    },
    changeWinClose() {
      ipcRenderer.send("close");
    },
    changeWinDirect(v) {
      ipcRenderer.send("window", v);
    }
    // changeWinHide(v) {
    //   if (v) return ipcRenderer.send("show");
    //   return ipcRenderer.send("hide");
    // }
  }
};
</script>

<style lang="less">
@import "../styles/color.less";

.bear {
  width: 100%;
  height: 100vh;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  color: @basicColor;
  background: #f4f4f4;
}
.bear-header {
  width: 100%;
  height: 30px;
  background: #fff;
  box-shadow: 0 1px 3px rgba(26, 26, 26, 0.1);
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.bear-header-title {
  flex: 1;
  -webkit-app-region: drag;
}
.bear-header-btngroup {
  display: flex;
  color: @basicColor;
  display: flex;
  align-items: center;
}
.bear-header-btngroup-handle {
  cursor: hand;
  cursor: pointer;
  margin: 0 2px;
}
.bear-content {
  width: 100%;
  height: calc(100vh - 58px);
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.bear-content-left {
  width: 40px;
  height: 100%;
  overflow: auto;
  /* overflow-y: auto; */
  background: #ffffff;
}
.bear-content-wrapper {
  flex: 1;
  height: 100%;
  overflow: hidden;
  overflow-y: auto;
  /* background: rgb(30, 30, 30); */
}
.bear-content-right {
  width: 300px;
  height: 100%;
  overflow: hidden;
  overflow-y: auto;
}
.bear-footer {
  width: 100%;
  height: 25px;
  overflow: hidden;

  // background: #181818;
  background: #fff;
  box-shadow: 0 -1px 3px rgba(26, 26, 26, 0.1);
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  font-size: 12px;
}
.bear-footer-version {
  line-height: 25px;
  padding-left: 10px;
}
.bear-footer-copyright {
  line-height: 25px;
  padding-right: 20px;
}
</style>
