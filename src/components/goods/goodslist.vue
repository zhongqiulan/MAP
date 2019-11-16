<template>
  <div>
    <el-menu
      :default-active="activeIndex2"
      class="el-menu-demo"
      mode="horizontal"
      @select="handleSelect"
      background-color="#545c64"
      text-color="#fff"
      active-text-color="#ffd04b"
    >
      <el-menu-item index="1">处理中心</el-menu-item>
      <el-submenu index="2">
        <template slot="title">我的工作台</template>
        <el-menu-item index="2-1">选项1</el-menu-item>
        <el-menu-item index="2-2">选项2</el-menu-item>
        <el-menu-item index="2-3">选项3</el-menu-item>
        <el-submenu index="2-4">
          <template slot="title">选项4</template>
          <el-menu-item index="2-4-1">选项1</el-menu-item>
          <el-menu-item index="2-4-2">选项2</el-menu-item>
          <el-menu-item index="2-4-3">选项3</el-menu-item>
        </el-submenu>
      </el-submenu>
      <el-menu-item index="3" disabled>消息中心</el-menu-item>
      <el-menu-item index="4">
        <a href="javascript:void(0)" target="_blank">订单管理</a>
      </el-menu-item>
      <el-menu-item index="5" @click="goHelpCenter()">
        <a href="javascript:void(0)">帮助中心</a>
      </el-menu-item>
    </el-menu>
    <div class="section">
      <div class="location">
        <span>当前位置：</span>
        <a href="#/" class="router-link-active">首页</a> &gt;
        <a href="#/site/goodslist" class="router-link-exact-active router-link-active">购物商城</a>
      </div>
    </div>
    <div class="section">
      <div class="wrapper">
        <div class="wrap-box">
          <div class="left-220" style="margin: 0px;">
            <div class="banner-nav">
              <ul>
                <li v-for="item in goods.catelist" :key="item.id">
                  <h3>
                    <i class="iconfont icon-arrow-right"></i>
                    <span>{{item.title}}</span>
                    <p>
                      <span
                        v-for="subitem in item.subcates"
                        :key="subitem.id"
                      >{{subitem.title}}&nbsp;</span>
                    </p>
                  </h3>
                  <div class="item-box">
                    <dl>
                      <dt>
                        <a href="/goods/40.html">{{item.title}}</a>
                      </dt>
                      <dd>
                        <a
                          v-for="subitem in item.subcates"
                          :key="subitem.id"
                          href="/goods/43.html"
                        >{{subitem.title}}</a>
                      </dd>
                    </dl>
                  </div>
                </li>
              </ul>
            </div>
          </div>
          <!--幻灯片-->
          <div class="left-705">
            <div class="banner-img">
              <el-carousel height="341px" :interval="3000" arrow="always">
                <el-carousel-item v-for="item in goods.sliderlist" :key="item.id">
                  <img :src="item.img_url" alt />
                </el-carousel-item>
              </el-carousel>
            </div>
          </div>
          <!--/幻灯片-->
          <div class="left-220">
            <ul class="side-img-list">
              <li v-for="(item,index) in goods.toplist" :key="item.id">
                <div class="img-box">
                  <label>{{index+1}}</label>
                  <img :src="item.img_url" />
                </div>
                <div class="txt-box">
                  <a href="/goods/show-98.html">{{item.title}}</a>
                  <span>{{item.add_time | dateFmt("YYYY-MM-DD")}}</span>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
    <div class="section" v-for="item in goodsgroup" :key="item.level1cateid">
      <div class="main-tit">
        <h2>{{item.catetitle}}</h2>
        <p>
          <a
            v-for="subitem in item.level2catelist"
            :key="subitem.subcateid"
            href="/goods/43.html"
          >{{subitem.subcatetitle}}</a>
          <a href="/goods/40.html">
            更多
            <i>+</i>
          </a>
        </p>
      </div>
      <div class="wrapper clearfix">
        <div class="wrap-box">
          <ul class="img-list">
            <li v-for="subitem in item.datas" :key="subitem.artID">
              <router-link :to="'/goodsinfo/'+subitem.artID" class>
                <div class="img-box">
                  <img v-lazy="subitem.img_url" />
                </div>
                <div class="info">
                  <h3>{{subitem.artTitle}}</h3>
                  <p class="price">
                    <b>{{subitem.sell_price}}</b>元
                  </p>
                  <p>
                    <strong>库存 {{subitem.stock_quantity}}</strong>
                    <span>
                      市场价：
                      <s>{{subitem.market_price}}</s>
                    </span>
                  </p>
                </div>
              </router-link>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.el-carousel__item img {
  width: 100%;
  height: 100%;
}
</style>

<script>
export default {
  data() {
    return {
      goods: {},
      goodsgroup: [],
      activeIndex: "1",
      activeIndex2: "1"
    };
  },
  created() {
    this.getGoodsData();
    this.getGoodsGroupData();
  },
  methods: {
    // 跳转到帮助中心页面
    goHelpCenter() {
      this.$router.push({
        //核心语句
        path: "/helpCenter", //跳转的路径
        query: {
          //路由传参时push和query搭配使用 ，作用时传递参数
          // id:this.id ,
        }
      });
    },
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
    },
    //获取我们购物商城头部的数据
    getGoodsData() {
      const url = `site/goods/gettopdata/goods`;

      this.$axios
        .get(url)
        .then(res => {
          this.goods = res.data.message;
        })
        .catch(err => {
          console.log(err);
        });
    },
    //获取商品分组的数据
    getGoodsGroupData() {
      const url = `site/goods/getgoodsgroup`;

      this.$axios.get(url).then(
        res => {
          this.goodsgroup = res.data.message;
        },
        err => {
          console.log(err);
        }
      );
    }
  }
};
</script>