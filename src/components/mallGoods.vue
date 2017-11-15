<template>
  <div class="good-item">
    <div style="">
      <div class="good-img">
        <router-link :to="'goodsDetails?productId='+msg.productId">
          <img :src="msg.productImageBig" :alt="msg.productName">
        </router-link>
      </div>
      <h6 class="good-title">{{msg.productName}}</h6>
      <h3 class="sub-title ellipsis">{{msg.sub_title}}</h3>
      <div class="good-price pr">
        <div class="ds pa">
          <router-link :to="'goodsDetails?productId='+msg.productId">
            <y-button class="btn" text="查看详情" style="margin: 0 5px;"></y-button>
          </router-link>
          <y-button text="加入购物车"
                    style="margin: 0 5px;"
                    @btnClick="addCart(msg.productId,msg.salePrice,msg.productName,msg.productImageBig)"
                    classStyle="main-btn"
          ></y-button>
        </div>
        <p><span style="font-size: 16px;">￥</span>
          {{msg.salePrice}}</p>
      </div>
    </div>
  </div>
 
</template>
<script>
import YButton from "/components/YButton";
import { addCart } from "/api/goods.js";
import { mapMutations, mapState } from "vuex";
export default {
  props: {
    msg: { type: [Object, Array] }
  },
  data() {
    return {};
  },
  methods: {
    ...mapMutations(["ADD_CART", "ADD_ANIMATION", "SHOW_CART"]),
    goodsDetails(id) {
      this.$router.push({ path: "goodsDetails/productId=" + id });
    },
    addCart(id, price, name, img) {
      if (!this.showMoveImg) {
        // 动画是否在运动
        if (this.login) {
          // 登录了 直接存在用户名下
          addCart({ productId: id }).then(res => {
            // 并不重新请求数据
            this.ADD_CART({
              productId: id,
              productPrice: price,
              productName: name,
              productImg: img
            });
          });
        } else {
          // 未登录 vuex
          this.ADD_CART({
            productId: id,
            productPrice: price,
            productName: name,
            productImg: img
          });
        }
        // 加入购物车动画
        var dom = event.target;
        // 获取点击的坐标
        let elLeft = dom.getBoundingClientRect().left + dom.offsetWidth / 2;
        let elTop = dom.getBoundingClientRect().top + dom.offsetHeight / 2;
        // 需要触发
        this.ADD_ANIMATION({
          moveShow: true,
          elLeft: elLeft,
          elTop: elTop,
          img: img
        });
        if (!this.showCart) {
          this.SHOW_CART({ showCart: true });
        }
      }
    }
  },
  computed: {
    ...mapState(["login", "showMoveImg", "showCart"])
  },
  mounted() {},
  components: {
    YButton
  }
};
</script>
<style lang="scss" rel="stylesheet/scss" scoped>
@import "../assets/style/mixin";
@import "../assets/style/theme";

.good-item {
    height: 330px;
  // border: 1px solid gold; 
  background: #fff;
  
  transition: all 0.5s; 
  &:hover {
    transform: translateY(-3px);
    box-shadow: 1px 1px 20px #999;
    .good-price p {
      display: none;
    }
    .ds {
      display: flex;
    }
  }
  .ds {
    @extend %block-center;
    width: 100%;
    display: none;
  }
  .good-img {
    img {
      width: 65%;
      margin: 20px auto;
      // border: 1px solid darkgoldenrod;    
      display: block;
    }
  }
  .good-price {
    margin: 15px 0;
    height: 30px;
    text-align: center;
    line-height: 30px;
    color: #e4393c;
    font-size: 20px;
  }
  .good-title {
    line-height: 1.2;
    font-size: 16px;
    color: #424242;
    margin: 0 auto;
    padding: 0 14px;
    text-align: center;
    overflow: hidden;
  }
  h3 {
    text-align: center;
    line-height: 1.2;
    font-size: 12px;
    color: #d0d0d0;
    padding: 10px;
  }
}
  @media screen and (max-width: 1000px) {
    .good-item{
        height: 330px;
    }
    .good-img{
      width: 70%;
       margin: 10px auto;
    }
  }
@media screen and (max-width: 500px){
  .good-item {
    height: 250px;
  background: #fff;  
  transition: all 0.5s; 
  .good-price p{
    font-size: 16px;
  }
   .good-title{
      font-size: 15px;
    }
  &:hover {
    transform: translateY(-3px);
    box-shadow: 1px 1px 20px #999;
    .good-price p {
      font-weight:bold;
      border:1px solid blue;
      display: block;      
    }
   
    .ds {
      display: none;
    }
  }

  .ds {
    // @extend %block-center;
    width: 100%;
    display: none;
    
  }
  
  
}
}




// .mall-goods{
//   display: flex;
//   height: 600px;
//   border: 1px solid black;
// }
</style>
