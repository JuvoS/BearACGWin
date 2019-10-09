<template>
  <div>
    <div>NGC 2024</div>
    <GridLife></GridLife>
    <div id class="ngc-pane"></div>
  </div>
</template>

<script>
export default {
  components: {
    GridLife: () => import("../../components/GridModel/Life")
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
