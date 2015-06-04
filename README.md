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
ul{
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
    font-size: 0.9rem; /* 设置字体相对根元素的大小 */
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

### 准备 "What I Do" 小节
挑战：

1. 使用css显示下划线
2. 使用css为技能添加图片

因为与内容无关的装饰应该使用css来实现。

#### 调节信息栏样式
```css
.info-section {
    background-color: #ffffff; /* 设置信息栏背景颜色 */
    padding: 30px 60px; /* 间接清除信息栏上下子元素折叠出的外边距 */
}
```

#### 为每个技能配图
以下元素会脱离文档流：

1. 定位的元素：`fixed`、`absolute`
2. 浮动元素：`float`
3. CSS背景图

对于能够事先得知空间大小的这里元素，可以使用`padding`来预留空间。
```css
.whatido__skill {
    padding-top: 100px; /* 内容使用内边距给背景图留下位置 */

    background-repeat: no-repeat; /* 背景图不重复 */
    background-position: center top; /* 背景图居中居顶放置 */
}

.whatido__skill--code {
    background-image: url(/img/skill-code.png); /* 设置code技能背景图 */
}

.whatido__skill--design {
    background-image: url(/img/skill-design.png); /* 设置design技能背景图 */
}

.whatido__skill--product {
    background-image: url(/img/skill-product.png); /* 设置product技能背景图 */
}
```

#### 三个技能的布局
使用`float`来布局三个技能：
```css
.whatido__skill-list {
    overflow: hidden; /* 强制容器有足够的高度包围飘动元素 */
}

.whatido__skill {
	...
    float: left; /* 向左浮动成为一行 */
    width: 33.33%; /* 三个元素平分一行空间 */
}
```

- 设置`overflow: hidden`后，css会把容器扩大到足够的高度以包含浮动元素。
- 也可以在最后的浮动元素后加个元素设置`clear: both`来撑开容器高度。
- 这里不用`display: inline-block`原因在于这个场景对空白敏感。

### 完善信息栏标题样式
```css
.info-section > header {
    text-align: center; /* 信息栏标题居中 */
    margin-bottom: 60px; /* 底部外边距留60像素 */
}

.info-section > header > h2 {
    font-size: 28px; /* 设置文字大小 */
    text-transform: uppercase; /* 转为大写 */
    letter-spacing: 3px; /* 字符间距 */
}

.info-section > header > h2:after {
    content: ""; /* 设置内容为空 */
    margin: 5px auto 0; /* 与标题保持距离且居中 */
    border-bottom: 2px solid black; /* 分割线 */
    width: 50px; /* 设置宽度 */
    display: block; /* 块级元素占一行 */
}

.info-section > header > h2:hover:after {
    width: 150px; /* 设置鼠标悬空宽度 */

    transition: width 0.5s ease-in-out; /* 宽度0.5秒生效 */
}

.info-section__description {
    font-style: italic; /* 信息栏标题描述斜体 */
}
```

## 第三天
### Float实现图文左右布局
目标：避免内容包围浮动元素
设置图片浮动：
```css
.education-experience__list > li > img {
    float: left; /* 向左浮动 */
    width: 150px; /* 设置宽度 */
}
```

`overflow: hidden`的作用：

1. 让容器适配浮动子元素高度
```css
.education-experience__list > li {
    overflow: hidden; /* 调节容器高度以包含浮动元素 */
}
```
2. 让浮动元素后的容器成为[block formatting context](http://www.w3.org/TR/CSS21/visuren.html#block-formatting)而不被浮动元素覆盖
```css
.education-experience__list__description {
    overflow: hidden; /* 禁止内容包围浮动元素 */
}
```

设置装饰性样式：
```css
.education-experience__list__description {
    overflow: hidden; /* 禁止内容包围浮动元素 */
}

.education-experience__list__description > h3 {
    font-size: 1.5rem; /* 增大字体 */
    letter-spacing: 2px; /* 扩大字符间距 */
    margin-bottom: 0; /* 清除底部外边距 */
}

.education-experience__title {
    margin-top: 0; /* 清除顶部外边距 */
    font-size: 1rem; /* 设置字体大小 */
    font-weight: 600; /* 加粗 */
}
```

### 设置Photos
#### CSS盒子模型
传统盒子模型（content-box）真实尺寸：

- real_height = height + padding + border
- real_width = width + padding + border

因此不能简单通过设置`width`和`height`来设计布局。

#### 全局使用border-box简化布局
可以通过设置全局的border-box模型来改变传统盒子模型。
border-box模型的好处是高宽的值都包括`padding`和`border`，设置`height`和`width`即为实际值。
设置全局border-box模型：
```css
html {
    box-sizing: border-box; /* 对根设置为border-box模型 */
}

*, *:before, *:after {
    box-sizing: inherit; /* 子元素继承父元素盒子模型以达到全局统一 */
}
```

上面代码与下面等价：
```css
* {
    box-sizing: border-box;
}
```
但后者有个缺点是当需要使用content-box时需要对目标容器下的所有元素重新设置样式，而前者只需要对目标元素设置即可。

#### 样式实现
```css
.photos__list {
    overflow: hidden; /* 撑开容器高度 */
}

.photos__list > li {
    float: left; /* 每一项向左浮动 */
    padding: 10px; /* 设置周围内边距为10像素 */
    width: 25%; /* 设置宽度为1/4个父容器宽以放置4个图片 */
}

.photos__list > li > img {
    width: 100%; /* 设置图片填满父容器 */
}
```

## 第四天
### 实现 Get In Touch
参照Photos实现即可：
```css
.get-in-touch__list {
    overflow: hidden; /* 为了留有足够高度容纳浮动元素 */
}

.get-in-touch__list > li {
    float: left; /* 向左浮动 */
    width: 25%; /* 一行放置4个元素 */
    padding: 10px; /* 设置间隔 */
    text-align: center; /* 文字居中 */
}
```

### Leave A Message表单布局
特点：

- 输入栏和提交按钮居中
- 输入栏标签在表单容器左侧，向右靠齐

装饰性样式：
```css
.contact input, .contact textarea {
    border: 1px solid #ccc; /* 设置边框 */
    border-radius: 4px; /* 设置边框圆角半径 */
}

.contact button {
    border: none; /* 去掉默认边框 */
    border-radius: 9999px; /* 边框圆角 */

    background: #ffd524; /* 底色黄色 */

    cursor: pointer; /* 鼠标样式为指针 */
    text-shadow: 0 1px 1px rgba(0, 0, 0, 0.2); /* 设置文字阴影为20% */
    color: #ffffff; /* 字体颜色为白色 */
    box-shadow: 0 3px 0 #daae1d; /* 盒子模型阴影 */
}
```

布局性样式：
```css
.contact input, .contact textarea {
    ...
    padding: 8px; /* 设置输入框内边距 */
    margin-bottom: 15px; /* 设置底部边距 */
    width: 100%; /* 宽度填满父容器 */
}

.contact button {
    ...
    padding: 6px; /* 设置按钮内边距 */
    width: 100%; /* 宽度填满父容器 */
}

.contact form {
    width: 40%; /* 表单容器宽度 */
    margin: 0 auto 50px; /* 块级元素居中 */
}
```

#### 子元素移到容器外与边靠齐
使用场景：

1. 有一个主要组件和一个附属组件
2. 在文档流中主要以主要组件布局
3. 附属组件位置相对主要组件布局

如：

- 输入栏和其标签
- 按钮和其菜单
- 组件和其提示框
- 容器内位置固定的组件（相册上一页和下一页）

注意：

- 父容器的定位不能是默认的`static`
- `top: 100%`和`left: 100%`指的是父容器的高度和宽度
- 绝对定位的元素需要设定宽度

#### 使用绝对定位布局文本框标签

1. 为每个输入框使用容器包裹：
    ```html
    <div class="input-area">
        <input name="name" id="name" type="text" />
        <label for="name">Name</label>
    </div>

    <div class="input-area">
        <label for="email">Email</label>
        <input name="email" id="email" type="email" />
    </div>

    <div class="input-area">
        <label for="message">Message</label>
        <textarea name="message" id="message"></textarea>
    </div>
	```
2. 父容器使用相对定位：
	```css
    .input-area {
        position: relative; /* 父容器使用相对定位 */
    }
	```
3. 设置标签布局：
    ```css
    .input-area {
        position: relative; /* 父容器使用相对定位 */
    }

    .input-area > label {
        position: absolute; /* 使用绝对定位 */
        top: 0; /* 与父容器顶部靠齐 */
        left: -100%; /* 向左偏移一个父容器宽度 */
        width: 100%; /* 设置宽度为父容器宽度与上面匹配 */
        padding: 8px; /* 与输入框有相同的内边距 */

        text-align: right; /* 文字向右对齐 */
    }
    ```