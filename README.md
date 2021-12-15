# Cascader

### 使用说明
* menu - Array - 必选参数  
  * menu: [{  
    * id: '', 可选，每个选项的唯一标识，建议加上  
    * title: '', 必选，选项文本内容  
    * constant: Any Type, 可选，当需要传递单个参数时直接传入，需要传入多个参数时通过对象的形式传入  
    * type: 'file', 可选，当type的值为'file'时为导入功能，方法自动传入三个参数，分别为response, file, fileList（参考el-upload文件上传成功时的钩子on-success）  
    * accept: '', 可选，导入功能文件类型限制  
    * child: [] 可选，子选项  
  * }]  
* text - String - 可选参数（按钮文字）  
* iconClass - String - 可选参数（按钮图标）  

### 代码说明
* `v-clickoutside`为element ui的自定义指令，用于定义目标节点外的点击事件，使用时需要先import。  
* id最好加上，el-cascader选中后会有高亮的效果，不加上id点击任意一项之后同级会全部高亮。这里点击之后再次打开没有显示高亮是因为使用了v-if对组件进行销毁，这会造成资源浪费，使用this.$refs.cascader中的方法消除高亮无效，最简单的方法就是直接加v-if  
* element ui的el-upload只有点击文本才有效果，这里更改了CSS样式，将点击范围调整到了一整行  
* 这里对el-cascader-panel的props进行了配置，默认子选项为value,label,children这里修改成了id,title,child是为了保证可以直接替换之前的下拉框组件，实际可以不用设置
