<template>
  <div class="good-container">
    <div class="goodsContainer">
    <!-- 左侧复选框和图片区域 -->
    <div class="left">
        <!-- 商品复选框 -->
        <input type="checkbox" class="checkbox" :id="'checkbox' + id" :checked="state" @change="stateChange">
        <!-- 商品的图片 -->
        <label :for="'checkbox' + id">
            <img :src="pic" alt="">
        </label>
    </div>
    <!-- 右侧商品详情与数量 -->
    <div class="right">
        <p class="title">{{ title }}</p>
        <!-- 商品的单价 -->
        <div class="unit-price">￥{{ price.toFixed(2) }}</div>
        <!-- 商品的数量模块 -->
        <!-- 插槽 -->
        <slot></slot>
    </div>
  </div>
  </div>
</template>

<script>
export default {
    // 自定义属性
    props: {
        // 商品的 id
        id: {
            required: true,
            type: Number
        },
        // 商品标题
        title: {
            default: '',
            type: String
        },
        // 商品图片
        pic: {
            default: '@/assets/logo.png',
            type: String
        },
        // 商品状态
        state: {
            default: false,
            type: Boolean
        },
        // 商品的单价
        price: {
            default: 0,
            type: Number
        },
        // 商品数量
        count: {
            default: 1,
            type: Number
        }
    },
    methods: {
        stateChange(e) {
            this.$emit('state-change' , { id: this.id , value: e.target.checked })
        }
    }
}
</script>

<style lang="less" scoped>
.goodsContainer {
    display: flex;
    width: 100%;
    height: 140px;
    border-bottom: 1px solid #ddd;
    .left {
        position: relative;
        flex: 4;
        .checkbox {
            width: 16px;
            height: 16px;
            position: absolute;
            bottom: 20px;
            left: 10px;
        }
        img {
            width: 100px;
            height: 100px;
            transform: translate(40px , 20px);
        }
    }
    .right {
        position: relative;
        flex: 6;
        .title {
            padding: 8px;
            font-size: 14px;
        }
        .unit-price {
            position: absolute;
            bottom: 20px;
            left: 15px;
            color: red;
        }
    }
}
</style>