<template>
  <div>
    <ul class="parent">
      <div v-for="(item, index) in dataList" :key="index" @click="dialogVisible = true">
        <li class="son">
          <span class="title">{{item.title}}</span>
          <br />
          <span class="content">{{item.content}}</span>
          <br />
          <el-button
            type="primary"
            v-if="item.sortNo==='1'"
            @click="sort(item.sortNo)"
            @click.stop
          >不禁止</el-button>

          <button class="cursor: not-allowed; background:#ccc！important" type="primary" v-else @click="sort(item.sortNo)" @click.stop>禁止</button>
        </li>
      </div>
    </ul>
    <el-dialog title="提示" :visible.sync="dialogVisible" width="30%" :before-close="handleClose">
      <span>这是一段信息</span>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dialogVisible: false,
      dataList: [
        {
          title: "将进酒",
          content:
            "君不见, 黄河之水天上来, 奔流到海不复回,君不见,高堂明镜悲白发, 朝如青丝暮成雪",
          sortNo: "0"
        },
        {
          title: "将进酒",
          content:
            "君不见, 黄河之水天上来, 奔流到海不复回,君不见,高堂明镜悲白发, 朝如青丝暮成雪",
          sortNo: "1"
        },
        {
          title: "将进酒",
          content:
            "君不见, 黄河之水天上来, 奔流到海不复回,君不见,高堂明镜悲白发, 朝如青丝暮成雪",
          sortNo: "1"
        },
        {
          title: "将进酒",
          content:
            "君不见, 黄河之水天上来, 奔流到海不复回,君不见,高堂明镜悲白发, 朝如青丝暮成雪",
          sortNo: "1"
        }
      ]
    };
  },
  methods: {
    sort(sortNo) {
      if (sortNo === "1") {
      alert("排序");
      }
    },
    handleClose(done) {
      this.$confirm("确认关闭？")
        .then(_ => {
          done();
        })
        .catch(_ => {});
    }
  },
  mounted() {}
};
</script>
<style scoped>
html * {
  margin: 0;
  padding: 0;
}

.parent {
  display: flex;

  flex-wrap: wrap;

  justify-content: center;
}
.son {
  flex: 0 1 300px;
  background-color: #fdf6e3;
  min-height: 200px;
  box-sizing: border-box;
  border: 3px solid #9db783;
  padding: 20px;
  margin: 20px;
}

.title {
  font-size: 20px;
  color: #c03035;
}

.content {
  font-size: 15px;
  color: #323232;
}
</style>
