<template>
  <div id="app">
    <el-menu
      :default-active="activeIndex2"
      class="el-menu-demo"
      mode="horizontal"
      @select="handleSelect"
      background-color="#545c64"
      text-color="#fff"
      active-text-color="#ffd04b"
    >
      <el-menu-item index="1" @click="goHome()">Home</el-menu-item>
      <el-submenu index="2">
        <template slot="title">我的工作台</template>
        <el-menu-item index="2-1">选项1</el-menu-item>
        <el-menu-item index="2-2">选项2</el-menu-item>
        <el-menu-item index="2-3">选项3</el-menu-item>
        <el-submenu index="2-4">
          <template slot="title">template</template>
          <el-menu-item index="2-4-1" @click="goPopTemplate()">popTemolate</el-menu-item>
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
    <transition name="fade" mode="out-in">
      <router-view></router-view>
    </transition>
  </div>
</template>

<script>
export default {
  name: "app",
  components: {},
  data() {
    return {
      activeIndex: "1",
      activeIndex2: "1",
    };
  },
  methods: {
     handleSelect(key, keyPath) {
      console.log(key, keyPath);
    },
    goPopTemplate(){
      this.$router.push({
        //核心语句
        path: "/popTemplate", //跳转的路径
        query: {
          //路由传参时push和query搭配使用 ，作用时传递参数
          // id:this.id ,
        }
      });
    },
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
       // 跳转到Home
    goHome() {
      this.$router.push({
        //核心语句
        path: "/goodslist", //跳转的路径
        query: {
          //路由传参时push和query搭配使用 ，作用时传递参数
          // id:this.id ,
        }
      });
    }
  }
};
</script>


<style lang="scss">
body {
  margin: 0px;
  padding: 0px;
  /*background: url(assets/bg1.jpg) center !important;
		background-size: cover;*/
  // background: #1F2D3D;
  font-family: Helvetica Neue, Helvetica, PingFang SC, Hiragino Sans GB,
    Microsoft YaHei, SimSun, sans-serif;
  font-size: 14px;
  -webkit-font-smoothing: antialiased;
}

#app {
  position: absolute;
  top: 0px;
  bottom: 0px;
  width: 100%;
}

.el-submenu [class^="fa"] {
  vertical-align: baseline;
  margin-right: 10px;
}

.el-menu-item [class^="fa"] {
  vertical-align: baseline;
  margin-right: 10px;
}

.toolbar {
  background: #f2f2f2;
  padding: 10px;
  //border:1px solid #dfe6ec;
  margin: 10px 0px;
  .el-form-item {
    margin-bottom: 10px;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.2s ease;
}

.fade-enter,
.fade-leave-active {
  opacity: 0;
}
</style>