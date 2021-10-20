# Bootstrap简介

Bootstrap框架能够帮助开发者通过简单的配置得到一个比较美观的页面，现在已经不仅是一个CSS框架，还有js代码，功能大体有：

1. 页面脚手架：
如样式重置、浏览器兼容、栅格系统和简单布局。

2. 基础CSS样式：
如代码高亮、排版、表单、表格和一些样式效果。

3. 组件：
如tab、pill、导航、弹窗、顶部栏和card等。

4. Javascript插件：
提供一些动态功能，如下拉菜单、模态窗口和进度条等。

## 一、网格
Bootstrap包含一个移动优先的响应式网格系统，在设计中可以包含多达12列，这些列设计为根据设备宽度相应地伸缩。

### （一）媒体查询
Bootstrap3默认定义了4种媒体查询的大小：

- 宽度小于768px像素的超小型设备，如手机，以`.col-xs-`为类前缀；
- 宽度小于768px的小设备，如平板电脑，以`.col-sm-`为类前缀；
- 宽度大于992px的中等尺寸设备，如小型桌面显示器，以`.col-md-`为类前缀；
- 宽度大于1200px的大型设备，如大型桌面显示器，以`.col-lg-`为类前缀。


### （二）创建网格

1. 创建容器，以容纳网格元素。选择固定宽度（使用`.container`类）或非固定宽度（使用`.container-fluid`类），可以将任何块级元素作为容器；
2. 设置行（使用`.row`类），以创建水平的列组；
3. 创建内容列（使用`.col-<media>-#`等类），每行包含12列，要为不同大小的设备创建不同的网格，只需在列元素上使用多个类即可，
   - 偏移：使用`.col-<media>-offset-#`类通过增加空白重定位列元素；
   - 排序：使用`.col-<media>-[pull|push]-#`类直接移动列元素，
4. 重置响应式列（使用`.clearfix`+在断点之间切换内容的响应式工具类`.hidden-md`、`.visible-md-inline-block`等）类，浮动元素后的元素都应该重置。



## 二、themes

### （一）标签和徽章

| 类             | 描述                       |
| -------------- | -------------------------- |
| .label         | 定义元素为标签             |
| .label-default | 设置标签元素为默认样式     |
| .label-primary | 设置标签元素为主标签样式   |
| .label-success | 设置标签元素为成功标签样式 |
| .label-info    | 设置标签元素为信息标签样式 |
| .label-warning | 设置标签元素为警告标签样式 |
| .label-danger  | 设置标签元素为危险标签样式 |
| .badge         | 定义元素为徽章             |



### （二）Well、面板和超大屏幕

| 类             | 描述                       |
| -------------- | -------------------------- |
| .well          | 定义元素为well             |
| .well-lg       | 设置well元素为大型well     |
| .well-sm       | 设置well元素为小型well     |
| .panel         | 定义元素为面板             |
| .panel-default | 将面板设置为默认样式       |
| .panel-primary | 将面板设置为成功主面板样式 |
| .panel-success | 将面板设置为成功面板样式   |
| .panel-info    | 将面板设置为信息面板样式   |
| .panel-warning | 将面板设置为警告面板样式   |
| .panel-danger  | 将面板设置为危险面板样式   |
| .panel-heading | 定义元素为面板标题         |
| .panel-body    | 定义元素为面板主体         |
| .panel-footer  | 定义元素为面板脚注         |
| .panel-title   | 定义元素为面板标题文本     |
| .jumbotron     | 定义元素超大屏幕           |



## 三、排版

### （一）标题类

| 类           | 描述                             |
| ------------ | -------------------------------- |
| .h1~.h6      | 设置标题样式，还可以作为内联标题 |
| .text-hide   | 隐藏文本创建图像替代             |
| .page-header | 创建页眉                         |



### （二）正文

| 类               | 描述                   |
| ---------------- | ---------------------- |
| .text-left       | 向左对齐文本           |
| .text-center     | 居中对齐文本           |
| .text-right      | 向右对齐文本           |
| .text-justify    | 分布文本               |
| .text-nowrap     | 关闭文本换行           |
| .pull-left       | 向左浮动显示元素       |
| .pull-right      | 向右浮动显示元素       |
| .center-block    | 居中块元素             |
| .text-muted      | 设置文本颜色，淡化     |
| .text-primary    | 设置文本颜色，表示主要 |
| .text-success    | 设置文本颜色，表示成功 |
| .text-info       | 设置文本颜色，表示信息 |
| .text-warning    | 设置文本颜色，表示警告 |
| .text-danger     | 设置文本颜色，表示危险 |
| .bg-primary      | 改变背景颜色，表示主要 |
| .bg-success      | 改变背景颜色，表示成功 |
| .bg-info         | 改变背景颜色，表示信息 |
| .bg-warning      | 改变背景颜色，表示警告 |
| .bg-danger       | 改变背景颜色，表示危险 |
| .text-capitalize | 将文本转换为首字母大写 |
| .text-lowercase  | 将文本转换为全小写     |
| .text-uppercase  | 将文本转换为全大写     |



### （三）其他

| 类                  | 描述                                   |
| ------------------- | -------------------------------------- |
| .list-unstyled      | 删除左外边距和列表样式                 |
| .list-inline        | 设置列表样式为内联                     |
| .dl-horizontal      | 设置定义列表样式为水平显示             |
| .initialism         | 稍微减小全大写缩略语的字体             |
| .lead               | 稍微增大文本                           |
| .small              | 稍微缩小字体                           |
| .blockquote-reverse | 右对齐引用语                           |
| .pre-scrollable     | 设置`<pre>`块最大高度为350并添加滚动条 |



## 四、表格

| 类                | 描述                                                         |
| ----------------- | ------------------------------------------------------------ |
| .table            | 定义元素为表格，默认样式为背景色透明，边框间隔为0，合并边框。 |
| .table-bordered   | 设置表格为所有单元格四周添加边框                             |
| .table-striped    | 设置表格有斑马纹                                             |
| .table-hover      | 设置表格为鼠标悬停于行上时为其添加背景颜色                   |
| .table-condensed  | 设置表格为所有单元格内边距减半                               |
| .table-responsive | 应用到表格周围的容器元素时，使表格能在较小的设备上水平滚动   |
| .active           | 将表格元素的背景更改为悬停颜色以表示活动字段                 |
| .success          | 将表格元素的背景更改为绿色，表示成功                         |
| .info             | 将表格元素的背景更改为蓝色，表示信息                         |
| .warning          | 将表格元素的背景更改为黄色，表示危险                         |
| .danger           | 将表格元素的背景更改为红色，表示警告                         |



## 五、表单

Bootstrap需要把每组标签和控件封装在`.form-group`类中，并对控件本身添加`.form-control`类。

通过`.form-control-static`类，可以给元素添加只读表单字段的效果。

```html
<form>
    <div class="form-group">
        <label for="firstName">First Name：</label>
        <input type="text" autofocus required id="firstName" placeholder="First Name" class="form-control">
    </div>
    <div class="form-group">
        <label for="lastName">Last Name：</label>
        <input type="text" autofocus required id="lastName" placeholder="Last Name" class="form-control">
    </div>
</form>
```



### （一）表单样式

| 样式     | 方法                                                         |
| -------- | ------------------------------------------------------------ |
| 水平表单 | 给`<form>`标签添加`.form-horizontal`类，给`<label>`元素添加`.control-label`类。 |
| 内联表单 | 给`<form>`标签添加`.form-inline`类。                         |
| 隐藏标签 | 给`<label>`元素添加`.sr-only`类。                            |



### （二）input类型

- checkbox，`.checkbox-inline`创建内联效果
- radio，`.radio-inline`创建内联效果
- color
- date
- week
- month
- datetime
- datetime-local
- email
- tel
- url
- number
- text
- password
- search



### （三）表单类

| 类               | 描述                                         |
| ---------------- | -------------------------------------------- |
| `.input-lg`      | 扩大控件。                                   |
| `.input-sm`      | 缩小控件。                                   |
| `.form-group-lg` | 扩大表单组所有元素大小。                     |
| `.form-group-sm` | 缩小表单组所有元素大小。                     |
| `.help-block`    | 定义描述表单字段的文本块（`<span>`等元素）。 |



### （四）控件属性

| 属性               | 说明                 |
| ------------------ | -------------------- |
| `aria-label`       | 虚拟标签？           |
| `aria-describedby` | 定义元素的帮助块id。 |