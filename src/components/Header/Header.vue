<template>
  <div class="header-container">
    <h2>我的购物车</h2>
  </div>
</template>

<script>
export default {};
</script>

<style lang="less" scoped>
.header-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 70px;
  background-color: blue;
  z-index: 999;
  h2 {
    text-align: center;
    line-height: 70px;
    font-size: 18px;
    color: #fff;
  }
}
</style>
