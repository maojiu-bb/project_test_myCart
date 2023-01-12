<template>
  <div class="counter-container">
    <!-- 商品数量 -->
    <button class="btn" @click="reduce">-</button>
    <span>{{ count }}</span>
    <button class="btn" @click="add">+</button>
  </div>
</template>

<script>
export default {
  props: {
    count: {
      default: 1,
      type: Number
    }
  },
  methods: {
    add() {
      this.$emit('countChange' , this.count + 1)
    },
    reduce() {
      if (this.count - 1 <= 0)
      return
      this.$emit('countChange' , this.count - 1)
    }
  }
}
</script>

<style lang="less" scoped>
.counter-container {
    position: absolute;
    right: 20px;
    bottom: 20px;
    .btn {
        width: 25px;
        height: 25px;
        border: 0;
        font-size: 16px;
    }
    span {
        font-size: 14px;
        padding: 0 10px;
    }
}
</style>