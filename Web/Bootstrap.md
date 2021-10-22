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





## 一、布局
Bootstrap包含一个移动优先的响应式网格系统，在设计中可以包含多达12列，这些列设计为根据设备宽度相应地伸缩。

### （一）媒体查询
Bootstrap3默认定义了4种媒体查询的大小：

- 宽度小于768px像素的超小型设备，如手机，以`.col-xs-`为类前缀；
- 宽度小于768px的小设备，如平板电脑，以`.col-sm-`为类前缀；
- 宽度大于992px的中等尺寸设备，如小型桌面显示器，以`.col-md-`为类前缀；
- 宽度大于1200px的大型设备，如大型桌面显示器，以`.col-lg-`为类前缀。



### （二）网格

#### 1. 行列

1. 创建容器，以容纳网格元素。选择固定宽度（使用`.container`类）或非固定宽度（使用`.container-fluid`类），可以将任何块级元素作为容器；
2. 设置行（使用`.row`类），以创建水平的列组；
3. 创建内容列（使用`.col-<media>-#`等类），每行包含12列，要为不同大小的设备创建不同的网格，只需在列元素上使用多个类即可，
   - 偏移：使用`.col-<media>-offset-#`类通过增加空白重定位列元素；
   - 排序：使用`.col-<media>-[pull|push]-#`类直接移动列元素，
4. 重置响应式列（使用`.clearfix`类），浮动元素后的元素都应该重置；



#### 2. 响应式工具

不同设备上可见性不同：

- `.hidden-md`
- `.visible-md-inline-block`、`.visible-md-inline`、`.visible-md-block`
- `.hidden-print`
- .`visible-print-inline-block`、`.visible-print-inline`、`.visible-print-block`



| 类            | 超小型设备 | 小型设备 | 中型设备 | 大型设备 |
| ------------- | ---------- | -------- | -------- | -------- |
| .hidden-xs    | 隐藏       | 可见     | 可见     | 可见     |
| .hidden-sm    | 可见       | 隐藏     | 可见     | 可见     |
| .hidden-md    | 可见       | 可见     | 隐藏     | 可见     |
| .hidden-lg    | 可见       | 可见     | 可见     | 隐藏     |
| .visible-xs-* | 可见       | 隐藏     | 隐藏     | 隐藏     |
| .visible-sm-* | 隐藏       | 可见     | 隐藏     | 隐藏     |
| .visible-md-* | 隐藏       | 隐藏     | 可见     | 隐藏     |
| .visible-lg-* | 隐藏       | 隐藏     | 隐藏     | 可见     |



### （三）排版

#### 1. 标题

| 类           | 描述                             |
| ------------ | -------------------------------- |
| .h1~.h6      | 设置标题样式，还可以作为内联标题 |
| .text-hide   | 隐藏文本创建图像替代             |
| .page-header | 创建页眉                         |



#### 2. 正文

| 类                 | 描述                                                 |
| ------------------ | ---------------------------------------------------- |
| .text-left         | 向左对齐文本                                         |
| .text-center       | 居中对齐文本                                         |
| .text-right        | 向右对齐文本                                         |
| .text-justify      | 分布文本                                             |
| .text-nowrap       | 关闭文本换行                                         |
| .pull-left         | 向左浮动显示元素                                     |
| .pull-right        | 向右浮动显示元素，必须设置明确的宽度                 |
| .center-block      | 居中块元素，必须设置明确的宽度                       |
| .text-muted        | 设置文本颜色，淡化                                   |
| .text-primary      | 设置文本颜色，表示主要                               |
| .text-success      | 设置文本颜色，表示成功                               |
| .text-info         | 设置文本颜色，表示信息                               |
| .text-warning      | 设置文本颜色，表示警告                               |
| .text-danger       | 设置文本颜色，表示危险                               |
| .bg-primary        | 改变背景颜色，表示主要                               |
| .bg-success        | 改变背景颜色，表示成功                               |
| .bg-info           | 改变背景颜色，表示信息                               |
| .bg-warning        | 改变背景颜色，表示警告                               |
| .bg-danger         | 改变背景颜色，表示危险                               |
| .text-capitalize   | 将文本转换为首字母大写                               |
| .text-lowercase    | 将文本转换为全小写                                   |
| .text-uppercase    | 将文本转换为全大写                                   |
| .sr-only           | 设置包含的内容仅对屏幕阅读器可见，对标准浏览器不可见 |
| .sr-only-focusable | 设置元素在得到焦点时再次显示                         |
| .show              | 内容对所有设备可见                                   |
| .invisible         | 内容在页面上不可见，但在内容流中占据空间             |



#### 3. 其他

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



### （四）导航

Bootstrap中的导航系统称作nav，在容器上使用`.nav`类可以创建一个nav，标准导航有`.nav-pills`和`.nav-tabs`两类。

```html
<nav role="navigation">
	<ul class="nav nav-pills">
        <li role="presentation" class="active"><a href="#">Home</a></li>
        <li role="presentation"><a href="#">About</a></li>
    </ul>
</nav>
```



#### 1. 下拉菜单

下拉菜单可以通过一个`.dropdown`类的容器构建，容器内包含有`.dropdown-toggle`类的按钮，然后用`.dropdown-menu`类添加菜单。建立下拉菜单后，需要添加jQuery和Bootstrap的js文件链接。



```html
<div class="dropdown">
    <button class="btn btn-default dropdown-toggle" data-toggle="dropdown">
        Choose one
        <span class="caret"></span>
    </button>
    <ul class="dropdown-menu">
        <li class="dropdown-header">Section 1</li>
        <li><a href="#">Item 1</a></li>
        <li><a href="#">Item 2</a></li>
        <li class="divider"></li>
        <li class="dropdown-header">Section 2</li>
        <li><a href="#">Item 3</a></li>
        <li><a href="#">Item 4</a></li>
    </ul>
</div>
```



菜单样式包括：

| 类                   | 描述               |
| -------------------- | ------------------ |
| .dropdown-menu-left  | 强制菜单左对齐容器 |
| .dropdown-menu-right | 强制菜单右对齐容器 |
| .dropdown-header     | 创建标题菜单项     |
| .divider             | 在菜单内创建分隔符 |



#### 2. 导航栏

```html
<nav class="navbar navbar-default">
	<div class="container-fluid">
        <div class="navbar-header">
            <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#collapsedNav">
                <span class="sr-only">Toggle navigation</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>
            <a href="#" class="navbar-brand">
            	<img src="logo.png" style="height:100%; width:auto;" alt="Logo" />
            </a>
            <p class="navbar-text">Logo</p>
        </div>
        
        <div class="collapse navbar-collapse" id="collapsedNav">
            <ul class="nav navbar-nav">
                <li class="active"><a href="#">Home</a></li>
                <li><a href="#">About</a></li>
                <li><a href="#">Search</a></li>
            </ul>
            <form class="navbar-form navbar-right" role="search">
                <div class="form-group">
                    <input type="text" class="form-control" placeholder="Search">
                </div>
            </form>
            <ul class="nav navbar-nav navbar-right">
                <li><a href="#">Contact Us</a></li>
            </ul>
        </div>
    </div>
</nav>
```



导航的样式包括：

| 类                   | 描述                                           |
| -------------------- | ---------------------------------------------- |
| .navbar-static-top   | 删除导航栏周围的内外边距，将其直接放在页面顶部 |
| .navbar-fixed-top    | 删除导航栏周围的内外边距，将其直接放在窗口顶部 |
| .navbar-fixed-bottom | 删除导航栏周围的内外边距，将其直接放在窗口底部 |
| .navbar-inverse      | 设置导航栏为暗色                               |
| .navbar-left         | 设置导航栏元素在左侧                           |
| .navbar-right        | 设置导航栏元素在右侧                           |
| .navbar-btn          | 设置为导航栏内的按钮样式                       |
| .navbar-text         | 设置为导航栏内的文本样式                       |
| .navbar-link         | 设置为导航栏内的链接样式                       |
| .navbar-form         | 设置为导航栏内的表单样式                       |
| .nav-justified       | 导航与容器等宽。                               |
| .nav-stacked         | 如果已经有.nav-pills类，可以得到垂直导航。     |
| .collapsed           | 设置该元素应该折叠显示                         |
| .collapse            | 表示该导航栏元素应该是可折叠组的一部分         |
| .iconbar             | 显示为条状图标                                 |



#### 3. 面包屑导航

```html
<ol class="breadcrumb">
    <li><a href="#">Item 1</a></li>
    <li><a href="#">Item 2</a></li>
    <li><a href="#">Item 3</a></li>
</ol>
```



#### 4. 分页

有页码：

```html
<ul class="pagination">
    <li>
    	<a href="#" aria-label="Previous"><span class="glyphicon glyphicon-arrow-left"></span></a>
    </li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li>
    	<a href="#" aria-label="Next"><span class="glyphicon glyphicon-arrow-right"></span></a>
    </li>
</ul>
```



无页码：

```html
<ul class="pager">
    <li class="previous">
    	<a href="#">
            <span class="glyphicon glyphicon-arrow-left">Previous</span>
        </a>
    </li>
    <li class="next">
    	<a href="#">
            <span class="glyphicon glyphicon-arrow-right">Next</span>
        </a>
    </li>
</ul>
```



#### 5. 列表组

列表组是可用于显示包含自定义内容的简单和复杂列表的一个组件，也可以作为垂直导航。

给列表`<ul>`标签添加`.list-group`类，给列表元素`<li>`标签添加`.list-group-item`类，可以进一步设置：

- `.list-group-item-heading`
- `list-group-item-text`



| 类                       | 描述               |
| ------------------------ | ------------------ |
| .list-group-item-success | 列表元素为成功样式 |
| .list-group-item-info    | 列表元素为信息样式 |
| .list-group-item-warning | 列表元素为警告样式 |
| .list-group-item-danger  | 列表元素为危险样式 |





## 二、themes、按钮

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



### （三）按钮

`<button>`、`<a>`、`<input type="button">`、`<input type="submit">`4类标签均可以创建按钮。

为容器添加`.btn-group`类可以创建按钮组，其role属性可为group或者toolbar。

为容器添加`.btn-toolbar`类可以创建工具栏。

bootstrap通过`.btn`和`.btn-<style>`类设置按钮样式，样式具体包括：

| 类                   | 描述                                       |
| -------------------- | ------------------------------------------ |
| .btn-default         | 标准按钮                                   |
| .btn-primary         | 一组按钮中的首选项                         |
| .btn-success         | 设置按钮为成功样式                         |
| .btn-info            | 设置按钮为信息样式                         |
| .btn-warning         | 设置按钮为警告样式                         |
| .btn-danger          | 设置按钮为危险样式                         |
| .btn-link            | 设置按钮为表现得链接                       |
| .btn-block           | 按钮为块级按钮，与父元素等宽               |
| .btn-lg              | 增大按钮                                   |
| .btn-sm              | 缩小按钮                                   |
| .btn-xs              | 大幅缩小按钮                               |
| .btn-group-lg        | 增大按钮组                                 |
| .btn-group-sm        | 缩小按钮组                                 |
| .btn-group-xs        | 大幅缩小按钮组                             |
| .btn-group-justified | 拉伸按钮组中的按钮，使其横跨整个容器的宽度 |
| .btn-group-vertical  | 水平堆叠按钮组中的按钮                     |
| .close               | 在容器右侧添加x符号。                      |



## 三、表格

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



## 四、表单

Bootstrap需要把每组标签和控件封装在`.form-group`类中，并对控件本身添加`.form-control`类。

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



### （一）样式

#### 1. 表单类型

| 样式     | 方法                                                         |
| -------- | ------------------------------------------------------------ |
| 水平表单 | 给`<form>`标签添加`.form-horizontal`类，给`<label>`元素添加`.control-label`类。 |
| 内联表单 | 给`<form>`标签添加`.form-inline`类。                         |
| 隐藏标签 | 给`<label>`元素添加`.sr-only`类。                            |



#### 2. 类样式 

| 类                   | 描述                                         |
| -------------------- | -------------------------------------------- |
| .input-lg            | 扩大控件。                                   |
| .input-sm            | 缩小控件。                                   |
| .input-group-lg      | 扩大输入组。                                 |
| .input-group-sm      | 缩小输入组。                                 |
| .form-group-l        | 扩大表单组所有元素大小。                     |
| .form-group-sm       | 缩小表单组所有元素大小。                     |
| .help-block          | 定义描述表单字段的文本块（`<span>`等元素）。 |
| .has-success         | 设置为成功状态。                             |
| .has-warning         | 设置为警告状态。                             |
| .has-error           | 设置为错误状态。                             |
| .form-control-static | 设置只读表单字段的效果。                     |



### （二）控件

#### 1. input类型

表单控件的标签主要为`<input`，此外还有`<textarea>`、`<select>`。bootstrap支持的input控件的`type`类型有：



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



#### 2. 输入组

输入组是一组元素，在输入控件的开始或者结束创建带有图表或文本的单独字段。

有些表单控件可以添加附加元素，输入组（`.input-group`和`.inputgroup-addon`类）为`<input>`控件添加附加字段。

```html
<div class="input-group">
    <label for="cost" class="sr-only">Amount</label>
    <span class="input-group-addon">
        <input type="checkbox" id="other" aria-label="Other" value="other">
    </span>
    <div class="input-group-addon">$</div>
    <div>
        <input type="number" required id="cost" placeholder="Amount" class="form-control">
    </div>
    <div class="input-group-addon">.00</div>
</div>
```



#### 3. 控件属性

| 属性             | 说明                       |
| ---------------- | -------------------------- |
| aria-label       | 虚拟标签？                 |
| aria-describedby | 定义元素的help-block的id。 |



### （三）交互

- focus（焦点）：常用于设置CSS样式。
- disabled（禁用）：作为表单控件属性。
- readonly（只读）：作为表单控件属性。
- validation（验证）



可以设置控件样式和反馈图标（`.has-feedback`和`.form-control-feedback`类）。

```html
<div class="form-group has-success has-feedack">
    <label for="textSuccess">Success</label>
    <input type="text" class="form-control" id="textSuccess" placeholder="Success">
    <span class="glyphicon glyphicon-ok form-control-feedback" aria-hidden="true"></span>
</div>
```





## 五、图像、媒体和图标

### （一）图像

| 类              | 描述                                       |
| --------------- | ------------------------------------------ |
| .img-responsive | 设置图像为响应式图像，在父元素中自动伸缩。 |
| .img-rounded    | 为图像提供圆角。                           |
| .img-circle     | 图像被裁剪成一个圆。                       |
| .img-thumbnail  | 图像周围有一个狭窄方框。                   |
| .thumbnail      | 设置在图像的容器上。                       |
| .caption        | 缩略图的描述性文本。                       |



### （二）媒体

`.media-list`类定义媒体列表，`.media`类定义媒体组、`.media-object`类定义媒体对象。



| 类                      | 描述                           |
| ----------------------- | ------------------------------ |
| .media-left             | 将媒体对象放在内容框左侧。     |
| .media-body             | 媒对象的主体内容。             |
| .media-heading          | 媒体对象的标题元素。           |
| .media-bottom           | 将媒体对象放在内容框底部。     |
| .media-middle           | 将媒体对象放在内容框垂直居中。 |
| .media-righ             | 将媒体对象放在内容框右侧。     |
| .caret                  | 在`<span>`中放置显示^符号。    |
| .embed-responsive       | 将媒体容器设置为响应式。       |
| .embed-responsive-16by9 | 定义媒体尺寸为16x9             |
| .embed-responsive-4by3  | 定义媒体尺寸为4x3              |
| .embed-responsive-item  | 将媒体设置为响应式。           |



### （三）Glyphicon

Glyphicon是一个包含260个图标的字体族，详情可以查看[官网](https://glyphicons.com/)。



```html
<span class="glyphicon glyphicon-hear-empty" aria-hidden="true"></span>
```



## 六、插件

### （一）模态窗口

模态窗口在特定时间内用程序强制用户交互，对应modal.js脚本。



#### 1. 触发

- js触发

```js
var options = {
    backdrop: true,
    keyboard: true,
    show: true
};
$('#myModal').modal(options);
```



- 数据属性触发

```html
<button type="button" class="btn" data-toggle="modal" data-target="#myModal">
    Click to Open a Modal
</button>
```



#### 2.  构建

为容器添加`.modal`类（还可以添加`.fade`类增加淡入效果），为窗口容器添加`.modal-dialog`类，为内容容器添加`.modal-content`。

```html
<div class="modal" id="myModal">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <button type="button" class="close" data-dismiss="modal" aria-label="close">
                    <span aria-hidden="true">&times;</span>
                </button>
                <h4 class="modal-title">my Modal</h4>
            </div>
            <div class="modal-body">             
                <p>Hello Modal!</p>
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-default" data-dismiss="modal">
                    Close
                </button>
            </div>
        </div>
    </div>
</div>
```



| 类        | 描述                                  |
| --------- | ------------------------------------- |
| .fade     | 设置在`.model`上，增加淡入效果        |
| .modal-lg | 设置在`.modal-dialog`上，增大模态窗口 |
| .modal-sm | 设置在`.modal-dialog`上，缩小模态窗口 |



#### 3. 方法

- toggle
- show：打开模态窗口
- hide：切换模态窗口
- handleUpdate：重新调整模态窗口定位



#### 4. 事件

- show.bs.modal：在调用show时触发
- showb.bs.modal：在模态窗口可见后触发
- hide.bs.modal
- hidden.bs.modal
- loaded.bs.modal

### 

### （二）附加导航

附加导航在页面上创建固定元素，用户滚动经过元素时，元素固定在屏幕上，对应affix.js插脚本。

为要固定的元素添加`data-spy="affix"`属性。



#### 1. 样式

- `.affix-top`
- `.affix`
- `.affix-bottom`



#### 2. 事件

- affix.bs.affix
- affixed.bs.affix
- affix-top.bs.affix
- affixed-top.bs.affix
- affix-bottom.bs.affix
- affixed-bottom.bs.affix



### （三）选项卡

一是需要1个用户选项卡栏的HTML，通常为带有`.nav`和`.nav-tabs`类的无序列表。

二是需要选项卡内容，通常为带有`.tab-content`的`<div>`容器，每个选项卡的`<div>`容器需要添加`.tab-pane`类。



#### 1. 触发

- 数据属性：设置`data-togle="tab"`属性
- js脚本

```js
$('#myTab a').tab('show');
```



#### 2. 事件

- hide.bs.tab
- hidden.bs.tab
- show.bs.tab
- shown.bs.tab



### （四）滚动监听

滚动监听（ScrollSpy）设置页面，使导航突出显示客户所读取的准确区域，当客户在页面上滚动时，导航中高亮显示的部分就会变化。



#### 1. 触发

- js脚本

```js
$('body').scrollspy({target: "#myNav"});
```



- 数据属性

为要固定的元素添加`data-spy="scroll"`属性，并添加指向导航元素的`data-target="#myNav"`，并确保body标记使用相对位置。



#### 2. 方法

每当删除或添加DOM元素时候，需要调用`.scrollspy('refresh')`方法。



#### 3. 事件

- activate.bs.scrollspy



### （五）工具提示和弹出框

工具提示（Tooltip）和弹出框（Popover）是出现在现有文本之上和周围的小内容块，使用tooltip.js和popover.js脚本。



#### 1. 触发

- 数据属性：添加`data-toggle="tooltip"`或`data-toggle="popover"`属性。

- js脚本

```js
$('[data-toggle]="tooltip"').tooltip()
$('[data-toggle]="popover"').popover()
```



#### 2. 选项

| 选项                | 取值                           | 作用                                 |
| ------------------- | ------------------------------ | ------------------------------------ |
| animation           | true、false                    | 是否应用CSS淡入淡出效果              |
| container           | 字符串或false                  | 为特定元素附加弹出框或工具提示       |
| delay               | 数字或对象                     | 延迟的毫秒数                         |
| html                | true、false                    | 是否允许将HTML插入弹出框或工具提示   |
| template            |                                | 创建弹出框或工具提示的代码模板       |
| placement           | top、right、bottom、left、auto | 定义显示弹出框或工具提示的位置       |
| selector            | 字符串或false                  | 允许动态HTML元素添加弹出框或工具提示 |
| title               | 字符串或函数                   | title属性未指定时的标题值            |
| content（仅弹出框） | 字符串或函数                   |                                      |
| trigger             | click、hover、focus、manual    | 设置触发方式                         |
| viewport            | 字符串或对象                   | 设置弹出框或工具提示的范围           |



#### 3. 事件

- show.bs.tooltip、show.bs.popover
- shown.bs.tooltip、shown.bs.popover
- hide.bs.tooltip、hide.bs.popover
- hidden.bs.tooltip、hidden.bs.popover



### （六）按钮

使用button.js脚本。



- `$().button('toggle')`：切换按钮状态
- `$().button('reset')`：重置按钮状态，将文本改回原始文本
- `$().button(string)`：将按钮文本切换为由字符串定义的 data-* 属性。



### （七）警告框

使用alert.js脚本。警告框用`.alert`类和一个上下文类创建，上下文类有：

- `.alert-success`
- `.alert-info`
- `.alert-warning`
- `.alert-danger`



如果希望读取警告框后撤销，需要添加`.alert-dismissible`类，并添加一个关闭按钮（需要具有`data-dismiss="alert"`属性）。



### （八）进度条

进度条通过创建包含`.progress`类的容器来构建，其中需要一个包含`.progress-bar`的容器。



```html
<div class="progress">
    <div class="progress-bar" role="progressbar" aria-valuenow="20" aria-valuemin="0" aria-valuemax="100" style="width:20%:">
        <span class="sr-only">20% Read</span>
    </div>
</div>
```



进度条的上下文类如下，此外还可以通过`progress-bar-striped`类添加条纹效果。

- `.progress-bar-success`
- `.progress-bar-info`
- `.progress-bar-warning`
- `.progress-bar-danger`



### （九）折叠

使用collapse.js脚本，同事需要安装Transition插件。



#### 1. 普通折叠

第一步是创建一个可折叠的容器，为容器添加`.collapse`类（如果是水平折叠，还要添加`.width`类），设置容器的id。

第二步是创建触发按钮，添加`data-toggle="collapse"`和`data-target="#targetID"`属性。



#### 2. 折叠面板

折叠面板（Accordion）是多个可折叠的部分，当面板的某个部分打开时，其余部分自动关闭。主要通过collapse插件的data-parent属性实现。



1. 创建一个带标题的面板（具有`.panel`类的容器），确保`.panel-heading`有唯一ID。
2. 用一个`<div>`容器包裹`.panel-body`，设置`.panel-collapse`和`.collapse`类。
3. 在`.panel-title`下创建链接`<a>`，并为链接添加`data-toggle="collapse"`和`data-parent="#myAccordion"`属性，从而创建触发器。
4. 用容器包裹整个面板，设置`.panel-group`类，确保ID与步骤3的`#myAccordion`一致。
5. 参考步骤1~3创建其他面板。



### （十）轮播

轮播包括轮播指标、幻灯片和控件三个部分，使用carousel.js脚本和Trasition插件。



1. 创建轮播容器，设置`.carousel`类、唯一ID和`data-ride="carousel"属性。`
2. 创建轮播指标（可选），这是一个设置为`.carousel-indicators`类的有序列表，每个列表项的`data-target`属性指向轮播容器的ID，`data-slide-to`包含幻灯片编号。
3. 创建幻灯片，这是一个设置为`.carousel-inner`类的容器，包含多个`.item`类的容器（其中一个再加上`.active`类），容器中的内容幻灯片图像或者信息。
4. 创建控件，这是放在轮播左右两侧的设置为`.carousel-control`类的`<a>`标签，，`href`属性指向轮播容器ID，往前翻页则添加`.left`类且`data-slide="prev"`，往后翻页则添加`.right`类且`data-slide=next`。





## 七、可访问性

| 属性             | 作用                   |
| ---------------- | ---------------------- |
| aria-controls    | 是否是控制元素         |
| aria-describedby | 告诉AT描述性文本的位置 |
| aria-expanded    | 是否是可扩展元素       |
| aria-hidden      | 告诉AT是否隐藏         |
| aria-invalid     | 告诉AT是否无效         |
| aria-label       | 指向由其标记的元素ID   |
| aria-labeledby   | 与aria-describedby类型 |
| aria-pressed     | 告诉AT是否被按下或激活 |
| role             | 告诉AT设备元素的目的   |
| title            | 元素的标题             |
