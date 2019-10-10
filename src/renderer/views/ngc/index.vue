<template>
  <div>
    <div>NGC 2024</div>

    <div id class="ngc-pane"></div>
    <el-button @click="drawer = true" type="primary">点我打开-测试Drawer</el-button>

    <!-- <GridLife></GridLife> -->
    <el-drawer
      title="我是标题"
      :visible.sync="drawer"
      :direction="direction"
      :before-close="handleClose"
    >
      <span>我来啦!</span>
    </el-drawer>
  </div>
</template>

<script>
export default {
  components: {
    GridLife: () => import("../../components/GridModel/Life")
  },
  data() {
    return {
      drawer: false,
      direction: "rtl"
    };
  },
  methods: {
    handleClose(done) {
      this.$confirm("确认关闭？")
        .then(_ => {
          done();
        })
        .catch(_ => {});
    }
  }
};
</script>

<style lang="less" scoped>
.ngc-pane {
  width: 480px;
  height: 320px;
  background: #ffffff;
  margin: 50px auto;
}
</style>
