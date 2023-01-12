<template>
  <div class="app-container">
    <!-- Header 头部区域 -->
    <Header></Header>
    <!-- Goods 主体区域 -->
    <Goods
      v-for="item in list"
      :key="item.id"
      :id="item.id"
      :title="item.goods_name"
      :pic="item.goods_img"
      :state="item.goods_state"
      :price="item.goods_price"
      :count="item.goods_count"
      @state-change="stateChange"
    >
    <!-- 插槽 -->
    <Counter :count="item.goods_count" @countChange="countChange(item , $event)"></Counter>
    </Goods>
    <!-- Footer 底部区域 -->
    <Footer :fullCheck="isFullCheck" :amount="amount" :total="total" @check-all="checkAll"></Footer>
  </div>
</template>

<script>
// 导入 axios 模块
import axios from "axios";
import Counter from '@/components/Counter/Counter.vue'
// 导入 Header 头部组件
import Header from "@/components/Header/Header.vue";
// 导入 Footer 底部组件
import Footer from "@/components/Footer/Footer.vue";
// 导入 Goods 商品组件
import Goods from "@/components/Goods/Goods.vue";

export default {
  data() {
    return {
      // 接收商品数据的，默认为空数组
      list: [],
    };
  },
  // 注册组件
  components: {
    Header,
    Footer,
    Goods,
    Counter
  },
  // 计算属性
  computed: {
    // 商品全选状态
    isFullCheck() {
      return this.list.every(item => item.goods_state)
    },
    // 计算商品总价
    amount() {
      return this.list.filter(item => item.goods_state).reduce((total , item) => total += item.goods_price * item.goods_count , 0)
    },
    // 计算商品的总件数
    total() {
      return this.list.filter(item => item.goods_state).reduce((total , item) =>  total += item.goods_count , 0)
    }
  },
  // 方法区域
  methods: {
    // 获取商品列表
    async initGoodsList() {
      const { data: res } = await axios.get("https://www.escook.cn/api/cart");
      if (res.status === 200) {
        this.list = res.list;
      }
    },
    // 全选
    checkAll(e) {
      this.list.forEach(item => {
          item.goods_state = e
      })
    },
    // 接收到商品状态的变化
    stateChange(e) {
      this.list.some(item => {
        if (item.id === e.id) {
          item.goods_state = e.value
          return
        }
      })
    },
    countChange(item , val) {
      item.goods_count = val
    }
  },
  created() {
    // 发起 Ajax 请求
    this.initGoodsList()
  },
};
</script>

<style lang="less" scoped>
.app-container {
  margin-top: 70px;
  margin-bottom: 70px;
}
</style>
