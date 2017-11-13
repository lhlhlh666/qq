<template>
  <div>     
      
        <div class="home-main">
              <!-- 轮播图 -->
            <section class="h-slide">
               
                 <div class="block">    
                    <el-carousel height="600px">
                        <el-carousel-item v-for="(item,i) in 2" :key="item"></el-carousel-item>                             
                    </el-carousel>
                </div>
                <div class="block2">    
                    <el-carousel height="407px">
                        <el-carousel-item v-for="(item,i) in 2" :key="item"></el-carousel-item>                             
                    </el-carousel>
                </div>
                <div class="block3">    
                    <el-carousel height="269px">
                        <el-carousel-item v-for="(item,i) in 2" :key="item"></el-carousel-item>                             
                    </el-carousel>
                </div>
                 <!-- 轮播图结束 -->              
                    <h1 class="h-slide-h1" style="">SPORTING GOODS</h1>
                    <router-link to="/goods"> <div class="home-cont">进入在线商城</div> </router-link>
                                 
            </section>
            <!-- =======关于我们========== -->

            <section>
              <div class="home-about-title">
                <span class="homt-abt-span">关于我们</span>
                <span style="">About us</span>
              </div>
                
                <div class="home-aboutus clearfix">
                
                    <aside class="home-abt-aside ">
                        <h1>SPORTING GOODS</h1>
                        <span>
                      在专栏设置面板中，您可以更换背景图片的
                      非常简单的，不需要任何别的设置
                      </span>
                      <div>查看详情</div>
                    </aside>
                    <div class="home-aboutus-img"></div>
               
                </div>
            </section>

            <!-- ==========热卖商品======= -->
            <section class="h-hot">
              <div class="h-hot-title">
                <span class="h-hot-title-span">热卖商品</span>
                <span>New product</span>
              </div>
              <div class="h-hot-product">              
                  <div class="h-hot-proGoods" v-for="(item,i) in computer" :key="item._id">
                    <div class="img">
                      <router-link :to="'goodsDetails?productId='+ item.productId">
                        <img :src="item.productImageBig" alt="">
                      </router-link>
                    </div>                    
                    <span>{{item.productName}}</span>
                    <p>¥ {{item.salePrice}}</p>
                  </div>  
              </div>
            </section>

            <!-- ================热点资讯（有资讯链接）================= -->
            <section class="h-hot">
              <div class="h-hot-title">
                <span class="h-hot-title-span">热点资讯</span>
                <span>New product</span>
              </div>
              <div class="home-hot-msg clearfix">             
                <aside v-for="(artic, index) in acticle" v-if="index<2" class="hot-msg-aside clearfix">                             
                  <div class="hot-msg-img clearfix">
                    <img :src="artic.imgcon" alt="">                 
                    <div>
                      <router-link :to="'/Articledetail?articleID=' + artic.articleID">
                      <h3 style="font-size:16px; font-weight: normal; color: #191919;margin-top: 20px;">{{artic.title}} </h3>  </router-link>
                      <span style="font-size:13px;color:#777777;margin-top: 15px;">发布日期： 2017-05-23</span>  
                      <p class="text" ref="text" style="font-size:13px;color:#777777;  margin-top: 20px;">{{artic.connect}}</p>
                     </div>
                  </div>                                     
                 
                               
                </aside>
                <div class="home-hot-img clearfix">
                  <img src="../../assets/img/h-hotimg.jpg" alt="">
                 </div>
              </div>
            </section>

            <!-- ===========================图片=============== -->
            
            <section class="home-bg home-bg-one">
              <div class="home-bg-msg">
                 <h1>SPORTING GOODS</h1>
                 <span>
                    在专栏设置面板中，您可以更换背景图片的<br>
                    非常简单的，不需要任何别的设置
                 </span>
              </div>
            </section>
            <section class="home-bg home-bg-two">
              <div class="home-bg-msg">
                 <h1>SPORTING GOODS</h1>
                 <span>
                    在专栏设置面板中，您可以更换背景图片的<br>
                    非常简单的，不需要任何别的设置
                 </span>
              </div>
            </section>
            <section class="home-bg home-bg-three">
              <div class="home-bg-msg">
                 <h1>SPORTING GOODS</h1>
                 <span>
                    在专栏设置面板中，您可以更换背景图片的<br>
                    非常简单的，不需要任何别的设置
                 </span>
              </div>
            </section>
        </div>
  </div>
</template>

<script>
import { getComputer } from "/api/goods.js";
import Header from "/common/header.vue";
import Footer from "/common/footer.vue";
import { getArticle } from '/api/articles';
// import mallGoods from "../comm/mallGoods.vue";
export default {
  data() {
    return {
      computer: [],
      productImageBig: [],
      acticle:[]
    };
  },
  components: {},
  methods: {
    _getComputer() {
      getComputer().then(res => {
        this.computer = res.result.data;
       
      });
    },
  
  _getActicle(){
    getArticle().then(res =>{
      this.acticle = res.data;
      //  console.log(this.acticle)
    })
  },
  Articledetail(id){
    this.$router.push({path: "goodsDetails/productId=" + id })
  },
},
  created() {
    this._getComputer();
    this._getActicle();
  },
mounted() {
    $(document).ready(function() {
      //限制字符个数
      // console.log('qqqqq')
      $(".text").each(function() {
        var maxwidth = 20;
        //  console.log('23435')
        if ($(this).text().length > maxwidth) {
          $(this).text(
            $(this)
              .text()
              .substring(0, maxwidth)
          );
         
          $(this).html($(this).html() + "...");
        }
      });
    });
  },
 
};
</script>

<style lang="css" rel="stylesheet/css" scoped>
.text{position: relative; line-height: 25px; max-height: 100px;overflow: hidden; font-size: 15px; color: gray}
.text::after{content: "..."; position: absolute; bottom: 0; right: 0; padding-left: 40px;
background: -webkit-linear-gradient(left, transparent, #fff 55%);
background: -o-linear-gradient(right, transparent, #fff 55%);
background: -moz-linear-gradient(right, transparent, #fff 55%);
background: linear-gradient(to right, transparent, #fff 55%);
}

.clearfix::after {
  content: "";
  display: block;
  clear: both;
  height: 0px;
  overflow: hidden;
}

el-carousel__item h3 {
  color: #475669;
  font-size: 14px;
  opacity: 0.75;
  line-height: 150px;
  margin: 0;
}

.el-carousel__item:nth-child(2n) {
  background-color: #99a9bf;
  background-image: url("../../assets/img/h-slide1.jpg");
  background-size: cover;
}

.el-carousel__item:nth-child(2n + 1) {
  background-color: #d3dce6;
  background-image: url("../../assets/img/h-slide2.jpg");
  background-size: cover;
}
.home-main {
  width: 100%;
  z-index: 0;
}
.block {
  z-index: 1;
}
.block2 {
  display: none;
}
.block3 {
  display: none;
}
.h-slide {
  width: 100%;
  text-align: center;
  position: relative;
}

.home-cont {
  width: 206px;
  height: 61px;
  margin: 0 auto;
  font-size: 15px;
  line-height: 61px;
  color: #001d5d;
  background-color: white;
  margin-top: 30px;
  position: absolute;
  top: 65%;
  left: 35%;
  right: 35%;
  bottom: 50%;
  z-index: 20;
  font-weight: 700;
}
.home-cont:hover {
  background-color: #3c7ff2;
  color: white;
  /* opacity: 0.5; */
}

.home-about-title {
  width: 1200px;
  margin: 0 auto;
  text-align: left;
  margin-top: 100px;
  border-bottom: 1px solid gainsboro;
}

.homt-abt-span {
  font-size: 22px;
  font-weight: bold;
  color: black;
}

.h-slide-h1 {
  width: 479px;
  height: 61px;
  margin: 0 auto;
  font-size: 50px;
  color: white;
  position: absolute;
  top: 50%;
  left: 35%;
  right: 35%;
  bottom: 50%;
  text-shadow: 0px 0px 2px gray;
  z-index: 20;
  /* border: 1px solid fuchsia; */
}

.home-aboutus {
  width: 100%;
}

.home-aboutus-img {
  width: 70%;
  float: right;
  height: 600px;
  background-image: url("../../assets/img/h-about.jpg");
}
.home-abt-aside {
  width: 30%;
  margin-top: 50px;
  color: black;
  float: left;
  position: relative;
}
.home-abt-aside h1 {
  width: 80%;
  font-size: 40px;
  position: absolute;
  left: 58%;
}
.home-abt-aside span {
  display: block;
  width: 46%;
  font-size: 14px;
  text-align: left;
  position: absolute;
  top: 100px;
  left: 66%;
}
.home-abt-aside div {
  width: 104px;
  height: 39px;
  line-height: 39px;
  text-align: center;
  border: 1px solid black;
  position: absolute;
  top: 150px;
  left: 66%;
}
.home-abt-aside div:hover {
  background-color: black;
  color: white;
  cursor: pointer;
}

/* =======热卖商品========= */
.h-hot {
  width: 1200px;margin: 0 auto;
  margin-top: 80px;
  margin: 0 auto;
  /* border: 1px solid red; */
}
.h-hot-title {
  width: 1200px;
  /* margin: 0 auto; */
  text-align: left;
  margin-bottom: 10px;
  border-bottom: 1px solid gray;
}
.h-hot-title-span {
  font-size: 22px;
  color: black;
  /* border-bottom: 2px solid slateblue; */
}

.h-hot-product {
  width: 1200px;
  /* margin: 0 auto; */
  /* margin-left: 40px; */
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
.h-hot-proGoods {
  width: 22%;
  margin-top: 20px;
  padding-bottom: 20px;
  border: 1px solid gainsboro !important;
}
.h-hot-proGoods:hover {
  box-shadow: 0 0 8px gray;
  margin-top: 18px;
}
.h-hot-proGoods .img {
  width: 100%;
  height: 70%;
}
.h-hot-proGoods img {
  width: 100%;
}
.h-hot-proGoods img:hover {
  /* transform: scale(1.2);   */
  overflow: hidden;
  transition: all 1s ease 0s;
  /* transition: all .6s ease;
        transition-property: all;
        transition-duration: 0.6s;
        transition-timing-function: ease;
        transition-delay: 0s; */
}

.h-hot-proGoods span {
  font-size: 18px;
  color: gainsboro;
  display: block;
  margin: 20px auto;
  /* border: 1px solid hotpink; */
}

.home-hot-msg {
  width: 1200px;
  margin: 20px auto;
  text-align: left;
  /* border: 1px solid gold; */
}
.hot-msg-aside {
  width: 730px;
  float: left;
  padding-top: 10px;
}
.hot-msg-img {
  width: 100%;
  border: 1px solid gray;
  margin-top: 25px;
  /* display: flex;  flex-wrap: wrap; justify-content: space-between; */
}
.hot-msg-img img {
  width: 38%;
  float: left;
  margin-right: 5px;
  /* margin: 8px; */
}
.home-hot-img {
  width: 35%;
  float: right;
  text-align: right;
  margin-top: -18%;
}
.home-hot-img img {
  width: 98%;
  /* margin-top: 15px; */
}

/* =============背景图片部分==================== */
.home-bg {
  width: 100%;
  position: relative;
  min-height: 100vh;
  background-repeat: no-repeat;
  background-size: cover;
  background-attachment: fixed;
  background-position: 0 0%;
}
.home-bg-one {
  background-image: url("../../assets/img/bg-1.jpg");
}
.home-bg-two {
  background-image: url("../../assets/img/bg-2.jpg");
}
.home-bg-three {
  background-image: url("../../assets/img/bg-3.jpg");
}
.home-bg-msg {
  width: 100%;
  color: white;
  position: absolute;
  top: 50%;
}
.home-bg-msg h1 {
  font-size: 40px;
  margin-bottom: 20px;
}
.home-bg-msg span {
  display: block;
  line-height: 25px;
}

@media screen and (max-width: 1000px) {
  .block {
    display: none;
  }
  .block2 {
    display: block;
  }
  .h-slide-h1 {
    margin: 0 auto;
    position: absolute;
    top: 50%;
    left: 25%;
    right: 35%;
    bottom: 50%;
  }
  .home-cont {
    margin-top: 80px;
  }

  .home-aboutus-img {
    width: 85%;
    height: 251px;
    float: none;
    background-size: cover;
    margin: 0 auto;
  }

  .home-abt-aside {
    width: 50%;
    margin-top: 50px;
    margin-left: -17%;
    float: left;
    /* position: relative; */
  }
  .home-abt-aside h1 {
    width: 100%;
    /* position: absolute; */
    left: 45%;
  }
  .home-abt-aside span {
    /* position: absolute; */
    top: 90px;
    left: 57%;
  }

  .home-abt-aside div {
    /* width: 104px; height: 39px; line-height: 39px; border: 1px solid black; */
    position: absolute;
    top: 150px;
    left: 57%;
  }
  .h-hot-product{
    width: 65%;
     margin: 0 auto;
    margin-left: 25px;
  }
  .h-hot-proGoods {
    width: 45%;
     margin: 0 auto;
    
  }

  .home-hot-msg {
    width: 90%;
    margin: 20px auto;
    text-align: center;
    border: 1px solid gold;
  }
  .hot-msg-aside {
    width: 80%;
    margin: 0 auto;
    float: none;
  }

  .home-hot-img {
    width: 60%;
    margin: 0 auto;
    float: none;
    text-align: center;
    margin-top: 26px;
  }
  .home-hot-img img {
    width: 100%;
  }
  .home-bg {
    min-height: 400px;
  }
}
@media screen and (max-width: 800px) {
  .home-aboutus-img {
    width: 100%;
    height: 251px;
    float: none;
    background-size: cover;
    margin: 0 auto;
  }
  .home-abt-aside {
    width: 100%;
    text-align: left;
  }
  .home-abt-aside h1 {
    width: 100%;
    left: 18%;
  }
  .home-abt-aside span {
    left: 18%;
  }
  .home-abt-aside div {
    position: absolute;
    top: 150px;
    left: 18%;
  }
  .home-about-title {
    width: 100%;
    margin: 0 auto;
    margin-top: 40px;
    margin-bottom: 20px;
    margin-left: 10px;
  }
  .h-hot-title {
    width: 100%;
    margin: 0 auto;
    margin-top: 40px;
    margin-bottom: 20px;
    margin-left: 10px;
  }
  .hot-msg-aside {
    width: 100%;
    float: left;
    padding-top: 10px;
  }

  .hot-msg-img {
    width: 100%;
    border: 1px solid gray;
    margin-top: 15px;
    text-align: left;
    padding-top: 10px;
    padding-bottom: 20px;
    /* display: flex;  flex-wrap: wrap; justify-content: space-between; */
  }
  .hot-msg-img img {
    width: 40%;
    margin: 0 auto;
    float: none;
    margin-left: 10px;
  }
}
@media screen and (max-width: 750px) {
  .block2 {
    display: none;
  }
  .block3 {
    display: block;
  }
  .h-slide-h1 {
    width: 300px;
    margin: 0 auto;
    font-size: 30px;
    position: absolute;
    top: 40%;
    left: 30%;
    right: 35%;
    bottom: 50%;
    /* position: absolute;  bottom: 0px; */
  }
   .h-hot-product{
    width: 100%;
     margin: 0 auto;
    margin-left: 0px;
  }
  .h-hot-proGoods {
    width: 50%;
     margin: 0 auto;
    
  }
  .home-cont {
    margin-top: 5px;
  }
  .home-abt-aside h1 {
    width: 100%;
    font-size: 100%;
    left: 18%;
  }
  .home-bg {
    background-attachment: scroll;
  }
  .home-bg-msg h1 {
    font-size: 20px;
  }
}
</style>
