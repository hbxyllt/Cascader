<template>
  <div v-clickoutside="hide" class="pull-left">
    <el-button style="position: relative;" @click="visible = true">
      <svg-icon
        :icon-class="iconClass"
        class-name="icon-svg"
      />
      <span>{{ text }}</span>
      <i class="el-icon-arrow-down el-icon--right" />
    </el-button>
    <el-cascader-panel
      v-if="visible"
      ref="cascader"
      :options="menu"
      :props="props"
      class="cascader_panel"
    >
      <template slot-scope="{ data }">
        <span v-if="data.methods">
          <span :class="data.type === 'file' ? 'upload' : ''" @click="visible = false">
            <el-upload v-if="data.type === 'file'" :action="Global.BASEURL" :accept="data.accept" :show-file-list="showFileList" :on-success="data.methods">
              {{ data.title }}
            </el-upload>
            <span v-else @click="data.methods(data.constant)">{{ data.title }}</span>
          </span>
        </span>
        <span v-else>{{ data.title }}</span>
      </template>
    </el-cascader-panel>
  </div>
</template>

<script>
import Clickoutside from 'element-ui/src/utils/clickoutside'
export default {
  name: 'Cascader',
  directives: { Clickoutside },
  props: {
    menu: {
      type: Array,
      default() { return [] }
    },
    iconClass: {
      type: String,
      default: '023菜单'
    },
    text: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      visible: false,
      props: {
        value: 'id',
        label: 'title',
        children: 'childer',
        expandTrigger: 'hover'
      },
      showFileList: false
    }
  },
  methods: {
    hide() {
      this.visible = false
    }
  }
}
</script>

<style scoped>
/* 保证下拉框浮动 */
.cascader_panel {
  position: absolute;
  z-index: 999;
  background-color: #fff
}
/* 清除el-cascader选中样式 */
/* .pull-left >>> .in-active-path {
  color: #606266;
  font-weight: 400;
} */
/* 将点击范围设置为一整行 */
.pull-left >>> .el-cascader-node {
  padding: 0 10px;
}
.pull-left >>> .el-cascader-node__label {
  padding: 0;
}
.pull-left >>> .el-cascader-node__label span {
  width: 100%;
  display: flex;
  position: relative;
}
/* 将导入功能点击范围设定为一整行 */
.upload {
  display: block !important;
  position: relative;
  width: 100%;
}
.upload >>> .el-upload {
  width: 100%;
  display: flex;
  position: relative;
}
</style>
