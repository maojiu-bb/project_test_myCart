<template>
  <div class="footer-container">
    <!-- 左侧全选框 -->
    <div class="left">
      <label for="checkbox-all"><span>全选</span></label>
      <!-- 全选按钮 -->
      <input type="checkbox" id="checkbox-all" :checked="fullCheck" @change="isFull" />
    </div>
    <!-- 中间总价格 -->
    <div class="mid">
        <p>合计：<span>￥{{ amount.toFixed(2) }}</span></p>
    </div>
    <!-- 右侧结算按钮 -->
    <div class="right">
        <button>结算({{ total }})</button>
    </div>
  </div>
</template>

<script>
export default {
    props: {
        // 全选状态
        fullCheck: {
            default: false,
            type: Boolean
        },
        // 总价
        amount: {
            default: 0,
            type: Number
        },
        // 总件数
        total: {
            default: 0,
            type: Number
        }
    },
    methods: {
        // 将全选状态传递出去
        isFull(e) {
            this.$emit('check-all' , e.target.checked)
        }
    }
};
</script>

<style lang="less" scoped>
.footer-container {
  display: flex;
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 70px;
  border-top: 1px solid #ddd;
  background-color: #fefefe;
  z-index: 9999;
}
.left {
    flex: 3;
    span {
        margin-left: 15px;
        line-height: 70px;
        font-size: 16px;
    }
    #checkbox-all {
        width: 16px;
        height: 16px;
        margin-left: 5px;
        vertical-align: middle;
    }
}
.mid {
    flex: 4;
    span {
        line-height: 70px;
        font-size: 16px;
        color: red;
    }
}
.right {
    flex: 3;
    button {
        width: 90px;
        height: 40px;
        margin-top: 15px;
        margin-left: 20px;
        border-radius: 20px;
        border: 0;
        background-color: blue;
        color: #fff;
        text-align: center;
        font-size: 14px;
    }
}
</style>
