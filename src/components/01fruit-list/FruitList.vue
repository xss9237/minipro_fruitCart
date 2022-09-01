<template>
    <div class="fruit-container">
        <!-- 头部标题 -->
        <div class="fruit-header">水果列表</div>
        <!-- 列表 -->
        <div class="fruit-list">
            <!-- 商品 -->
            <div class="fruit-item" v-for="item in fruitlist" :key="item.id">
                <!-- 左侧 input+图片 -->
                <div class="left form-check">
                    <input class="form-check-input" type="checkbox" :id="item.id" v-model="item.state" />
                    <label class="form-check-label" :for="item.id">
                        <!-- 图片 -->
                        <img :src="item.pic" alt class="thumb" />
                    </label>
                </div>
                <!-- 右侧 名称+价格+数量 -->
                <div class="right">
                    <!-- 名称 -->
                    <h5 class="top">{{item.fruit}}</h5>
                    <!-- 价格+数量 -->
                    <div class="bottom">
                        <!-- 价格 -->
                        <div class="price">￥{{item.price.toFixed(2)}}</div>
                        <!-- 数量 -->
                        <div class="btns">
                            <button class="btn btn-light" @click="onSubClick(item.id)">-</button>
                            <div class="count">{{item.count}}</div>
                            <button class="btn btn-light" @click="onAddClick(item.id)">+</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- 底部结算 -->
        <div class="footer">
            <!-- 总数量 -->
            <div class="counts">总数量：{{counts}}个</div>
            <div class="prices">总价：{{amount}}元</div>
            <button type="button" class="btn btn-primary" :disabled="isDisabled">结算</button>
        </div>
    </div>
</template>
<script>
import { computed } from '@vue/runtime-core'
export default {
  name: 'FruitList',
  data() {
    return {
      fruitlist: [
        {
          id: 1,
          fruit: '香橼',
          pic: '/src/assets/images/1.jpg',
          price: 5,
          count: 1,
          state: true
        },
        {
          id: 2,
          fruit: '柚子',
          pic: '/src/assets/images/2.jpg',
          price: 4.5,
          count: 1,
          state: false
        },
        {
          id: 3,
          fruit: '橘子',
          pic: '/src/assets/images/3.jpg',
          price: 3,
          count: 1,
          state: false
        },
        {
          id: 4,
          fruit: '橙子',
          pic: '/src/assets/images/4.jpg',
          price: 6,
          count: 1,
          state: false
        },
        {
          id: 5,
          fruit: '粑粑柑',
          pic: '/src/assets/images/5.jpg',
          price: 6.5,
          count: 1,
          state: false
        },
        {
          id: 6,
          fruit: '柠檬',
          pic: '/src/assets/images/6.jpg',
          price: 4,
          count: 1,
          state: false
        },
        {
          id: 7,
          fruit: '青柠',
          pic: '/src/assets/images/7.jpg',
          price: 5.2,
          count: 1,
          state: false
        }
      ]
    }
  },
  methods: {
    // 点击了- 按钮
    onSubClick(id) {
      const findResult = this.fruitlist.find((x) => x.id === id)
      if (findResult && findResult.count > 1) {
        findResult.count--
      }
    },
    // 点击了 + 按钮
    onAddClick(id) {
      const findResult = this.fruitlist.find((x) => x.id === id)
      if (findResult) {
        findResult.count++
      }
    }
  },
  computed: {
    counts() {
      let t = 0
      this.fruitlist.forEach((x) => {
        if (x.state) {
          t += x.count
        }
      })
      return t
    },
    amount() {
      let s = 0
      this.fruitlist
        .filter((x) => x.state)
        .forEach((x) => {
          s += x.price * x.count
        })
      return s
    },
    // 控制按钮是否禁用 判断总数量是否为0
    isDisabled() {
      return this.counts === 0
    }
  }
}
</script>
<style lang="less" scoped>
.fruit-container {
  .fruit-header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 45px;
    line-height: 45px;
    background-color: #0078d7;
    text-align: center;
    color: #fff;
    font-size: 13px;
    font-weight: 700;
    z-index: 999;
  }
  .fruit-list {
    margin: 45px 0 50px 0;
    .fruit-item {
      display: flex;
      padding: 5px;
      border-bottom: 1px solid #eee;
      .left {
        margin-right: 10px;
        .form-check-input {
          margin-top: 42px;
          border-radius: 5px;
        }
        .thumb {
          width: 100px;
          height: 100px;
        }
      }
      .right {
        display: flex;
        flex: 1;
        flex-direction: column;
        justify-content: space-between;
        .top {
          font-weight: 700;
        }
        .bottom {
          display: flex;
          justify-content: space-between;
          .price {
            color: red;
            font-weight: 700;
            font-size: 13px;
          }
          .btns {
            display: flex;
            align-items: center;
            .count {
              border: none;
              outline: none;
              width: 28px;
              text-align: center;
            }
          }
        }
      }
    }
  }
  .footer {
    display: flex;
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 50px;
    line-height: 50px;
    text-align: center;
    justify-content: space-between;
    align-items: center;
    padding: 0 10px;
    background-color: #fff;
    font-size: 13px;
    button {
      width: 50px;
      height: 30px;
      outline: none;
    }
  }
}
</style>