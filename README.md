# 思客前端学习
[TOC]

## 第一天
### HTML模版建议
#### 基础建议

1. 设置*doctype*
2. 设置页面编码
3. 引入初始化css

#### 扩展建议

1. 指定使用HTML5语法
2. 要求 IE 遵守现代浏览器的渲染标准
3. 锁死页面在移动设备显示宽度
4. 引入了[normalize.css](http://jerryzou.com/posts/aboutNormalizeCss/), 在默认的HTML元素样式上提供了跨浏览器的高度一致性

### 固定背景
固定背景两种实现方式：

1. 元素固定，背景不做特殊处理
2. 背景固定，元素不做特殊处理
```css
body {
    background-image: url("/img/bg5.jpg"); /* 设置背景图片 */
    background-attachment: fixed; /* 背景固定不滚动 */
    background-size: cover; /* 背景图片填满整个屏幕 */
    background-position: center; /* 背景图片居中 */
}
```

### 居中外包围框
#### 作用

1. 居中内容
2. 让围框中的block元素充满父容器宽度，以便支持响应式布局

### 实现原理

1. 使用div包括内容
2. 设置宽度为960px
	> 你常常会看到网页选择960px这个宽度，这是因为一般浏览器是1024宽，加上滚动条就是1000-1004。960给滚动条和其他浏览器UI预留了住够的空间。 并且960这个数字可 2，3，4，5，6，8，10，12等数字除尽，方便做grid。
3. 设置`margin: 0 auto;`

### 头部容器
该页面头部包含头像和标题，其中头像居中并向上溢出头部容器。

#### HTML元素简单分类

1. [块级元素](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Block-level_elements)：`p`、`div`、`h1`、`h2`、`table`、`ol`等
	- 浏览器在元素前后添加断行，元素默认宽度填满父容器。

2. [行元素](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Inline_elemente)：`span`、`img`、`a`、`button`、`input`等
	- 一般用在文字流中使用，不会添加断行，默认内容撑开宽度。

##### 居中块级元素
设置宽度和margin：
```css
.block {
    width: 960px;
    margin: 0 auto;
}
```

##### 居中行级元素
设置display将其变成块级元素并按块级元素方式居中：
```css
.inline {
	display: block;
    width: 960px;
    margin: 0 auto;
}
````

##### 使用父容器居中
使用父容器来设置居中会影响这个容器的所有元素：
```css
.container {
	text-align: center;
}
```

### 实现头部容器
1. 语义化页面元素，使用`header`标签定义头部容器
2. 居中头像和`h1`标题
```css
.main-header {
    background-image: url("/img/banner.jpg"); /* 设置背景图片 */
    text-align: center; ./* 居中容器内容 */
}
```

3. 在最后引入Open Sans字体
```html
<link href='http://fonts.useso.com/css?family=Open+Sans:400,300' rel='stylesheet' type='text/css'>
```

4. 更新`.main-header`字体属性
```css
.main-header {
    background-image: url("/img/banner.jpg"); /* 设置背景图片 */
    text-align: center;  /* 居中容器内容 */
    font-weight: 300; /* 设置字体粗细 */
    font-size: 20px; /* 设置字体大小 */
    font-family: 'Open Sans','helvetica',arial,sans-serif; /* 设置使用字体优先级 */
    text-shadow: 0 1px rgba(0,0,0,0.3); /* 设置字体阴影 */
}
```

5. 头像修饰
```css
.main-header__avatar {
    box-shadow: 0 0 2px 1px rgba(0,0,0,0.2); /* 给头像加阴影 */
    border-radius: 999px; /* 变成圆形边框 */
    width: 150px;
    border: 2px solid #ffffff;
}
```

6. 更新头部容器样式
```css
.container {
	...
    padding-top: 1px; /* 防止和子元素折叠外边距 */
}

.main-header {
	...
    margin-top: 70px; /* 设置头部容器外边距 */
    padding-bottom: 1px; /* 防止和标题折叠外边距 */
}

.main-header__avatar {
	...
    margin-top: -70px; /* 使头像溢出头部容器 */
    margin-bottom: 10px; /* 设置头像下外边距 */
}

.main-header h1 {
    margin: 0 0 20px; /* 设置标题外边距 */
}
```

### CSS属性排序
1. 定位属性：`position`、`float`、`z-index`、`clear`
2. 盒模型属性：`padding`、`margin`、`display`、`width`、`height`、`border`、
3. 字体相关
4. CSS2视觉相关：`background`
5. CSS3属性：`border-radius`、`box-shadow`

## 第二天
### 设置全局字体风格
```css
body {
    font-family: 'Open Sans','helvetica',arial,sans-serif; /* 设置使用字体优先级 */
    color: #62686f; /* 默认字体颜色 */
}

h1, h2, h3, h4, h5, h6 {
    color: #333;  /*标题字体颜色 */
    font-weight: 300; /* 设置字体粗细 */
}
```

### 语义化HTML标签
HTML5定义了一套语义化标签：

- `header`：头部模块
- `nav`：导航模块
- `article`：文章模块
- `section`：文章节
- `footer`：底部模块

语义化HTML标签可以分离内容和页面样式，规范化页面结构。
实现页面模块的基本步骤：

1. 了解模块职能（定义语义）
2. 组织HTML代码
3. 观察模块布局需求
4. 组织CSS代码

### 设置导航栏
```html
<nav class="main-nav">
    <ul>
        <li><a href="#">Work</a></li>
        <li><a href="#">Experience</a></li>
        <li><a href="#">Photos</a></li>
        <li><a href="#">Contact</a></li>
    </ul>
</nav>
```

消除列表默认样式：
主要对无序列表的列表样式和左边距进行清除，同时由于`li`是块级元素，通过display设置为行级元素。
```css
nav > ul{
    list-style: none; /* 对无序列表消除默认列表样式 */
    padding-left: 0; /* 消除无序列表默认左边距 */
    margin: 0; /* 消除无序列表默认外边距 */
}

nav > ul > li {
    display: inline; /* 将li设置为行内元素 */
}
```

其他样式：
```css
.main-nav {
    background-color: #333; /* 导航背景颜色 */
}

.main-nav ul li {
    margin: 15px 10px; /* 设置外边距 */
}

.main-nav ul li a {
    color: #fff; /* 导航字体颜色为白色 */
    font-size: 0.9rem; /* 设置字体大小 */
    font-weight: 300;  /* 设置字体粗细 */
    text-transform: uppercase; /* 内容变为大写 */
    text-decoration: none; /* 去掉下划线 */
}

.main-nav ul li a:hover {
    text-decoration: underline; /* 悬停时出现下划线 */
}
```

注意此时`.main-nav ul li`设置的上下外边距不会生效，原因在于行元素不能设置垂直方向的距离，包括：`padding`、`margin`、`height`。
若想垂直方向设置的距离属性生效，可以将其`display`设置为`inline-block`，`inline-block`会让其对外表现为行元素，对内表现为块元素：
```css
nav > ul > li {
    display: inline-block; /* 将项放置到一行 */
}
```