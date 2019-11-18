<template>
  <div>
    <div class="column">
      <div class="column-left">
        <div class="resize-bar"></div>
        <div class="resize-line"></div>
        <div class="resize-save">
          <el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick"></el-tree>
        </div>
      </div>
      <div class="column-right">
        <a href="#div1">div1</a>
        <a href="#div2">div2</a>
        <a href="#div3">div3</a>
        <a href="#div4">div4</a>
        <a href="#div5">div5</a>

        <div id="div1" style="width: 60px;height: 300px;background-color: #003366">1</div>

        <div id="div2" style="width: 60px;height: 300px;background-color:#556699">2</div>

        <div id="div3" style="width: 60px;height: 300px;background-color: #f5f5f5">3</div>

        <div id="div4" style="width: 60px;height: 300px;background-color: #7d7d7d">4</div>

        <div id="div5" style="width: 60px;height: 300px;background-color: #e9f1fa">5</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dialogVisible: false,
      data: [
        {
          label: "一级 1",
          children: [
            {
              label: "二级 1-1",
              children: [
                {
                  label: "三级 1-1-1"
                }
              ]
            }
          ]
        },
        {
          label: "一级 2",
          children: [
            {
              label: "二级 2-1",
              children: [
                {
                  label: "三级 2-1-1"
                }
              ]
            },
            {
              label: "二级 2-2",
              children: [
                {
                  label: "三级 2-2-1"
                }
              ]
            }
          ]
        },
        {
          label: "一级 3",
          children: [
            {
              label: "二级 3-1",
              children: [
                {
                  label: "三级 3-1-1"
                }
              ]
            },
            {
              label: "二级 3-2",
              children: [
                {
                  label: "三级 3-2-1"
                }
              ]
            }
          ]
        }
      ],
      defaultProps: {
        children: "children",
        label: "label"
      }
    };
  },
  methods: {
    handleNodeClick(data) {
      console.log(data);
    }
  },
  mounted() {}
};
</script>
<style scoped>
.column {
  overflow: hidden;
}

.column-left {
  height: 100vh;
  background-color: #fff;
  position: relative;
  float: left;
}

.column-right {
  height: 100vh;
  padding: 16px;
  background-color: #eee;
  box-sizing: border-box;
  overflow: hidden;
}

.resize-save {
  position: absolute;
  top: 0;
  right: 5px;
  bottom: 0;
  left: 0;
  padding: 16px;
  overflow-x: hidden;
}

.resize-bar {
  min-width: 20vw;
  height: inherit;
  resize: horizontal;
  cursor: ew-resize;
  opacity: 0;
  overflow: scroll;
}

/* 拖拽线 */
.resize-line {
  position: absolute;
  right: 0;
  top: 0;
  bottom: 0;
  border-right: 2px solid #eee;
  border-left: 1px solid #bbb;
  pointer-events: none;
}

.resize-bar:hover ~ .resize-line,
.resize-bar:active ~ .resize-line {
  border-left: 1px dashed skyblue;
}

.resize-bar::-webkit-scrollbar {
  width: 200px;
  height: inherit;
}

/* Firefox只有下面一小块区域可以拉伸 */
/* @supports (-moz-user-select: none) {
  .resize-bar:hover ~ .resize-line,
  .resize-bar:active ~ .resize-line {
    border-left: 1px solid #bbb;
  }

  .resize-bar:hover ~ .resize-line::after,
  .resize-bar:active ~ .resize-line::after {
    content: "";
    position: absolute;
    width: 16px;
    height: 16px;
    bottom: 0;
    right: -8px;
    background: url(./resize.svg);
    background-size: 100% 100%;
  }
} */
</style>
