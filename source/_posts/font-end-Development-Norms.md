---
title: font-end Development Norms
date: 2016-09-01 13:55:27
tags:
  - Development
  - Norms
  - Font-end
  - javascript
  - css
  - html
---

网鱼 - 计费组: 前端攻城狮 dubin@wywk.cn

wechat: [@hivandu](https://github.com/hivandu)   --> [blog](http://hivan.me)


**PS: 由于时间仓促，本文档并不完善。后续将进行持续更新。 如果是在本地locahost查看博客文档，可能图片不能展现，这个时候需要下载PDF进行查看。所以每次维护此文档更新后，需要生成一次PDF方便其他人员下载查看**

此手册主要实现的目标：代码一致性和最佳实践。通过代码风格的一致性，降低维护代码的成本以及改善多人协作的效率。同时遵守最佳实践，确保页面性能得到最佳优化和高效的代码。

此手册是在开发中积累下来的经验和参考其它规范/指南制定的，它只是起指导作用，除个别条目强制之外，大多数为非强制约束，开发者可根据自己的实际情况自行决定是否要遵守 该指南只是保证大方向一致性和最佳实践的阶段性总结，不是最后结论，它会随着时间而变化。

<!-- more -->

## 简介

所谓规范，乃是需要大家遵守的标准。为了项目的可维护性，以及前端团队的建设，特撰写此规范。
此规范主要目标： 代码一致性和最佳实践。通过代码风格的一致性，降低维护代码的成本以及提高多人协作的效率。同时遵守最佳实践，确保页面性能得到最佳优化和高效的代码。
此规范的实施：此规范是在阿树的前端手册基础上，融合了大家的经验并参考其它规范/指南制定的，有很强的指导作用， 如无特殊情况，前端人员都需要遵守此规范 。
此规范的更新：该规范只是保证大方向一致性和最佳实践的阶段性总结，不是最后结论，它会随着时间而变化。
此版本的第一版是根据阿树的 [前端开发规范手册](http://zhibimo.com/read/Ashu/front-end-style-guide/) 和 ZOL前端规范1.1 修改而来，感恩他们。

## 基本原则

#### 结构、样式、行为分离

尽量确保文档和模板只包含 `HTML` 结构，样式都放到样式表里，行为都放到脚本里。

#### 缩进

统一**Tab**缩进（总之缩进统一即可），不要使用 空格 或者 Tab、空格混搭。`indent_size : 2`

#### 文件编码

**使用不带 BOM 的 UTF-8 编码**。

- 在 HTML中指定编码 `<meta charset="utf-8">`；
- 无需使用 `@charset` 指定样式表的编码，它默认为 UTF-8 （参考 [@charset](https://developer.mozilla.org/en-US/docs/Web/CSS/@charset)）；

#### 一律使用小写字母
```vbscript-html
<!-- Recommended -->
<img src="google.png" alt="Google">

<!-- Not recommended -->
<A HREF="/">Home</A>
```

```scss
/* Recommended */
color: #e5e5e5;

/* Not recommended */
color: #E5E5E5;
```

#### 省略外链资源 URL 协议部分

省略外链资源（图片及其它媒体资源）URL 中的 http / https 协议，使 URL 成为相对地址，避免 [Mixed Content](https://developer.mozilla.org/en-US/docs/Security/MixedContent) 问题，减小文件字节数。

**其它协议（ftp 等）的 URL 不省略。**

```vbscript-html
<!-- Recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>

<!-- Not recommended -->
<script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>
```

```css
/* Recommended */
.example {
  background: url(//www.google.com/images/example);
}

/* Not recommended */
.example {
  background: url(http://www.google.com/images/example);
}
```

#### 统一注释

通过配置编辑器，可以提供快捷键来输出一致认可的注释模式。

**HTML 注释**

- 模块注释
```vbscript-html
<!-- 文章列表列表模块 -->
<div class="article-list">
...
</div>
```
- 区块注释

```vbscript-html
<!--
@name: Drop Down Menu
@description: Style of top bar drop down menu.
@author: Ashu(Aaaaaashu@gmail.com)
-->
```

**CSS 注释**

样式表总体注释 -- 声明样式表的相关信息（主要包括样式表的 **描述 、 作者 、 创建/更新时间 、 版本号** ）
```scss
/**  
 * @Description: the stylesheet of XXX 
 * @authors: xxx (xxx@fengniao.com)
 * @date:    2015-10-12 10:57:15
 * @version: 1.0
 */
```

组件块和子组件块以及声明块之间使用一空行分隔，子组件块之间两空行分隔；

```css
/* selector */
.selector {padding: 15px; margin-bottom: 15px;}

/* selector-secondary */
.selector-secondary {display: block; /* 注释*/}
.selector-three {display: span;}


/* selector-secondary */
.selector-secondary {display: block; /* 注释*/}
.selector-three {display: span;}
```

**JavaScript 注释**

- 单行注释
必须独占一行。`//` 后跟一个空格，缩进与下一行被注释说明的代码一致。
```javascript
function fun(a,b,c){
  var a = 1;
  
  // 我是注释
  return {
    b=2, c=3
  }
}　
```
- 多行注释
避免使用 /*...*/ 这样的多行注释。有多行注释内容时，使用多个单行注释。

- 函数/方法注释
- 函数/方法注释必须包含函数说明，有参数和返回值时必须使用注释标识。；
- 参数和返回值注释必须包含类型信息和说明；
- 当函数是内部函数，外部不可访问时，可以使用 @inner 标识；
```javascript
/**
 * 函数描述
 *
 * @param {string} p1 参数1的说明
 * @param {string} p2 参数2的说明，比较长
 *     那就换行了.
 * @param {number=} p3 参数3的说明（可选）
 * @return {Object} 返回值描述
 */
function foo(p1, p2, p3) {
    var p3 = p3 || 10;
    return {
        p1: p1,
        p2: p2,
        p3: p3
    };
}
```

- 文件注释
文件注释用于告诉不熟悉这段代码的读者这个文件中包含哪些东西。 应该提供文件的大体内容, 它的作者, 依赖关系和兼容性信息。如下:

```javascript
/**
 * @fileoverview Description of file, its uses and information
 * about its dependencies.
 * @author user@meizu.com (Firstname Lastname)
 * Copyright 2015 Meizu Inc. All Rights Reserved.
 */
```

#### 代码验证

- 使用 [W3C HTML Validator](http://validator.w3.org/) 来验证你的HTML代码有效性；
- 使用 [W3C CSS Validator](http://jigsaw.w3.org/css-validator/validator.html.zh-cn) 来验证你的CSS代码有效性；
代码验证不是最终目的，真的目的在于让开发者在经过多次的这种验证过程后，能够深刻理解到怎样的语法或写法是非标准和不推荐的，即使在某些场景下被迫要使用非标准写法，也可以做到心中有数。

## 目录结构和文件命名
建立统一的目录结构和使用规范的文件命名有助于其他人查看切片结果，有利于后端开发人员迅速的找到需要的 html、图片、样式和脚本文件等。

#### 目录结构

|目录|存放文件|命名规则|
|:----|:-----|:-----|
|`html`|HTML|文件使用合适的英文来命名|
|`images`| 图片文件 | 根据包含内容的英文来命名|
|`css`|样式文件|根据样式特点、功能的英文来命名|
|`js`|脚本文件| 根据功能的英文来命名|
　

#### 文件命名

-  HTML 文件：
  - 页面文件命名以小写英文单词（或域名）命名，尽量不用缩写（除非是约定俗成或通用的缩写）。 例如： 论坛可以使用 forum.html、 bbs.html。
  - 分页面命名格式为：频道名-内页名，单词全部小写。其中“内页名”规则同第一条。 例如：手机论坛可以使用 forum-phone.html、 forum-mobile.html、 bbs-phone.html等）。
- 图片文件： 根据拼图的内容决定名称，例如 icon.png。
- CSS 文件： 当只有一个 CSS 文件时，可根据频道或 HTML 文件来命名；当存在多个CSS 文件时，应根据 CSS 文件的功能来命名，各页面单独使用 CSS 根据页面名称来命名。 常见命名范例：
  - 通用功能或模块： common.css/global.css/base.css
  - 主要模块或功能： master.css/main.css
  - 布局： layout.css
  - 打印： print.css
  - ...

#### 开发工具

好的开发工具提供了便捷的操作和丰富的智能提示，能极大的提高开发效率。但是应使用开发工具的代码编辑、代码格式化和文件管理功能，而不应使用开发工具所见即所得编辑功能。 可以使用自己认为习惯或合适的开发工具，这里不做特殊要求，但应注意**版权问题**。

## 图片

#### 切片

切片结果需满足：最大程度的符合设计稿效果；尽可能小的文件大小。 网页中所有和内容无关的装饰性的图片都应该使用背景图片或图片字体；而和内容有关的图片都不得使用背景图。
在切片时，如遇到内容/广告等图片，可以使用公用的示例图片：

![Alt text](./1472620615664.png)

#### 图片格式

网页中所有的图片应使用 PNG-8、 PNG-24、 GIF 、 JPEG 和 base64 格式。

| 格式 | 扩展名 | 特点、使用场景和注意事项 |
|:----|:----:|:--------|
| PNG-8 | `.png` |默认使用的格式，支持透明，只支持 256 种颜色索引，几乎所有的切片图片都应使用此格式。PNG格式在部分版本 Chrome浏览器下有 BUG，在拼图时有时需要适当留有间距。|
|PNG-24| `.png` | 支持 8 位 256 级透明度。主要用于有半透明效果的图片。 |
|GIF|`.gif`| 和 PNG-8 类似，但在多数时候文件稍大（像素图通常比 PNG-8 小），而兼容性最好。GIF 支持多帧动画，在需要动画图片时，或同样的图片文件比 PNG-8 尺寸较小时使用此格式。|
|JPEG|`.jpg`| 不支持透明色。用于色彩较为丰富、需要过渡自然的大幅面Banner。JPEG 是有损压缩格式，因此在输出时请选择一个最能满足设计效果而文件大小又最小的压缩率|
|base64|`data:image/jpeg;base64`| H5页面用的较多 |

#### 使用 CSS3 和 IE 滤镜、空标签代替图片

在 CSS3 和 IE 滤镜都能达到设计效果时，使用它们来代替图片。这些方式能减少网络载入时间，并易于修改。可斟酌不同的项目适当采用。

#### Sprites

CSS Sprites 是在当前宽带互联网条件下，为了减少 HTTP 请求数量，降低对服务器压力，提高页面加载速度而使用的一项技术。
> CSS Sprites 核心是将多个装饰背景图片组合到一张图片上，然后使用 CSS 的 background-position 来控制需要显示的部分。

CSS Sprites 在使用不当时可能造成维护麻烦、占有太多的客户端内存、颜色失真、显示临近图片内容等问题。

> 图片在客户端通常会先初始化为 Bitmap 对象，然后进行渲染、显示，所以其占用内存计算方式为图片的 高宽4，而一张 4000*3000 的图片将占用客户端 45M 的内存——这在开发移动终端网页时尤为需要注意。

基于以上特点，使用 CSS Sprites 应遵循以下规范：
- 图标：将实际位于左侧的图标放在右侧，而实际位于右侧的图标放在左侧，而多个图标尽量错位排列；但是对于不定宽度的容器内的右侧图标除外。
- 为图标留出适量的空白，除非确定图标只在尺寸和该图标完全一致的固定容器中显示。
- 尽量不使用 background-position 的 right 或 bottom 来定位，因为当拼图需要修改尺寸时它们将失效；但是对于不定宽度的容器内的右侧图标除外。
- 当网页中的各种背景和装饰性图标颜色较为丰富，超过 256 色所能表现而需要将图片进行拆分。拆分时将颜色相近或相同的元素拼接在一张图片内，这将减少颜色索引数，从而减少文件大小；也能在 256 色的范围内提供更为丰富的颜色表现。
- 避免拼图尺寸过大。
- 避免单张拼图文件过大，单张图片大小应不大于 20KB。当需要拆分时，按照颜色相近、元素类型相近和网页屏幕占用的规则来进行。

#### 优化

所有的图片结果在文件较大时应进行优化（小于 1.5KB 时不需要），在保证达到设计效果的情况下达到最小的文件大小。
> 在使用 Photoshop CS 存储为 WEB 使用格式时，默认保存了大量的元数据。这会是输出的图片文件增加 1-2KB。 在输出无法利用优化的图片时， 请保证下图所示的选项选择为“无”：

![Alt text](./1472696460174.png)

##HTML
尽量遵循 HTML 标准和语义，但是不要以牺牲实用性为代价。任何时候都要尽量使用最少的标签并保持最小的复杂度。

### 2.1 通用约定
#### 标签

- 自闭合（self-closing）标签，无需闭合 ( 例如： img input br hr 等 )；
- 可选的闭合标签（closing tag），需闭合 ( 例如：</li> 或 </body> )；
- 尽量减少标签数量，注意保持一定的**可扩展性**；
```vbscript-html
<img src="images/google.png" alt="Google">
<input type="text" name="title">

<ul>
  <li>Style</li>
  <li>Guide</li>
</ul>

<!-- Not recommended -->
<span class="avatar">
  <img src="...">
</span>

<!-- Recommended -->
<img class="avatar" src="...">
```

**标签使用补录 （大招）：**

除了标签应具有语义化特征外，还应该在使用上符合以下规范：
- **空标签**： 尽量不要有空标签，除非为了网页的特殊效果需要或为了兼容低版本浏览器而不得不这样定义（例如清除浮动、半透明背景等）。
- **A** ： 必须为A添加 href 属性，否则就不应该使用A标签。
- **IMG**： 必须为标签添加 alt 属性。 除非有脚本希望计算图片原始大小，必须为IMG设定高度和宽度（有时可仅设置其中一项）以防止抖动。可以使用 CSS、行内 style、 width/height 属性来设置。
- **DL DD DT** ： DL中的DT和DD不需要一一对应，但多数情况下应在它们一一对应时使用，否则可能存在滥用。
- **FORM** ： 表单对象应包含在FORM标签内，除非页面必须依赖 AJAX 来实现。但是请不要为FORM 定义样式，并且FORM标签不得参与页面布局。
- **LABEL** ： 当表单的输入框、单选框、复选框、多行文本框、下拉选项等有标签文字时，必须将这些文字用LABEL标签包含，并使用 FOR 属性进行连接。
- **TABLE** ： 当内容是表格形式时，应果断使用table。 可以使用 table 的 border-spacing/ border-collapse 样式、单元格的 padding 样式来取代表格的 cellspacing 和 cellpadding 属性，因此上应该只能具有 id、class、 summary 和自定义的属性。 建议为表格添加 summary 属性作为表格的说明，它可被屏幕阅读器识别，也可作为模块识别标志。 完整的table标签如下：

```html
<table summary="表格的说明">
  <caption>标题</caption>
      <colgroup>
      <col class="name" />
  <col />
  </colgroup>
  <thead>
      <tr>
      <th>名称</th>
      <th>操作</th>
      </tr>
  </thead>
  <tfoot>
      <tr><td colspan="2">第一页</td></tr>
  </tfoot>
  <tbody>
      <tr><td></td><td></td></tr>
      <tr><td></td><td></td></tr>
  </tbody>
</table> 
```

合理的利用表格的这些标签将为我们开发提供便利。
表头应使用th作为单元格标签。
- **LINK** ： 链接外部样式表： `<link href="css/sky.css"rel="stylesheet" />`， 不再需要类型声明（如果需要，请添加媒体选择属性）；必须放在head标签内。
- **STYLE** ： 页内样式： `style.../style`；必须放在head标签内， 不再需要类型声明。
- **SCRIPT** ： 不应为`<script>`标签添加 language 属性， 也不再需要为标签定义 type 属性。
  - 链接外部脚本：` <script src="js/jquery.js"></script>`；尽量放在需要使用之前一行。
  - 页内脚本： `<script>...</script>`；放置在需要使用处。多数情况下，应位于</body>前。

#### SEO 和预留

- SEO 相关 为搜索引擎优化预留 h1 和 h2 标签：在此类标签上定义 class 来定义样式。
- 属性预留 除非表单对象和框架，不得使用 name 属性。 为 JavaScript 开发和表单对象预留 id 属性：除非所有 JavaScript 由前端组完成，尽量不使用 id 选择器（ #）。

#### Class 与 ID

- class 应以功能或内容命名，不以表现形式命名；
- class 与 id 单词字母小写，多个单词组成时，采用中划线-分隔, 如果一定要使用id，采用驼峰规则；
- 使用唯一的 id 作为 Javascript hook, 同时避免创建无样式信息的 class；

```html
<!-- Not recommended -->
<div class="j-hook left contentWrapper"></div>

<!-- Recommended -->
<div id="j-hook" class="sidebar content-wrapper"></div>
```

#### 属性顺序

HTML 属性应该按照特定的顺序出现以保证易读性。

- id
- class
- name
- data-xxx
- src, for, type, href
- title, alt
- aria-xxx, role

```html
<a id="..." class="..." data-modal="toggle" href="###"></a>

<input class="form-control" type="text">

<img src="..." alt="...">
```

#### 引号

属性的定义，统一使用双引号。

```html
<!-- Not recommended -->
<span id='j-hook' class=text>Google</span>

<!-- Recommended -->
<span id="j-hook" class="text">Google</span>
```
#### 嵌套

`a 不允许嵌套 div`这种约束属于语义嵌套约束，与之区别的约束还有严格嵌套约束，比如`a 不允许嵌套 a`。

严格嵌套约束在所有的浏览器下都不被允许；而语义嵌套约束，浏览器大多会容错处理，生成的文档树可能相互不太一样。

**语义嵌套约束**

- `<li>` 用于 `<ul>` 或` <ol> `下；
- `<dd>`, `<dt>` 用于 `<dl> `下；
- `<thead>`, `<tbody>`, `<tfoot>`, `<tr>`, `<td>` 用于 <table> 下；

**严格嵌套约束**

- inline-Level 元素，仅可以包含文本或其它 inline-Level 元素;
- `<a>`里不可以嵌套交互式元素`<a>`、`<button>`、`<select>`等;
- `<p>`里不可以嵌套块级元素`<div>`、`<h1>~<h6>`、`<p>`、`<ul>/<ol>/<li>`、`<dl>/<dt>/<dd>`、`<form>`等。

更多详情，参考[WEB标准系列-HTML元素嵌套](http://www.smallni.com/element-nesting/)

#### 布尔值属性

HTML5 规范中 `disabled`、`checked`、`selected` 等属性不用设置值。
```html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

**HTML字符**
HTML 字符： 特殊字符应尽量使用 HTML 定义的字符而不是直接使用文字；使用HTML 字符时，可以使用十进制编码格式或已有命名的实体，推荐使用前者。完整的HTML 字符集请参考附录：[常用 HTML 字符](http://www.w3school.com.cn/tags/html_ref_entities.html)。


#### HTML模板（大招）

- utf-8 模板

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Title</title>
        <meta name="keywords" content="" />
        <meta name="description" content="" />
        <link href="css/metro.css" rel="stylesheet" />
    </head>
    <body>
        ...
    </body>
</html> 
```

- gbk模板
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="gbk" />
        <title>Title</title>
        <meta name="keywords" content="" />
        <meta name="description" content="" />
        <link href="css/metro.css" rel="stylesheet" />
    </head>
    <body>
        ...
    </body>
</html>
```


### 语义化
没有 CSS 的 HTML 是一个语义系统而不是 UI 系统。

通常情况下，每个标签都是有语义的，所谓语义就是你的衣服分为外套， 裤子，裙子，内裤等，各自有对应的功能和含义。所以你总不能把内裤套在脖子上吧。-- 一丝

此外语义化的 HTML 结构，有助于机器（搜索引擎）理解，另一方面多人协作时，能迅速了解开发者意图。

#### 常见标签语义
| 标签 |  语义 |
| :----- | :------ |
|`div`|主要用于布局，排版和分割页面的结构|
|`span`|  没有特殊的意义，可以用作排版的辅助，然后在 CSS 中定义 span|
|`ul`|  无序列表|
|`ol`|  有序列表|
|`li`|  列表项目|
|`dl`|  定义列表|
|`dt`|  定义列表的标题|
|`dd`|  定义列表的描述|
|`h1-h6`| 标题（ 根据重要性依次递减， h1 是最重要的标题）|
| `<p>`   | 段落    |
|`img`|图片内容|
|`q`|引用|
|`a`|链接|
|`input`|按钮，输入框，选择框|
| `<blockquote>` | 大段引用 |
| `<cite>`| 一般引用 |
| `<b>` | 为样式加粗二加粗 |
|`<strong>`| 为强调内容而加粗 |
| `<i>` | 为样式倾斜而倾斜 |
| `<em>` | 为强调内容而倾斜 |
| `<code>`| 代码标识 |
|`<abbr>`| 缩写 |
|`adress`|地址|

#### 常用HTML5标签

|标签|用途|
|:---|:---|
|`section`|模块|
|`header`|页头、模块头|
|`footer`|页尾、模块尾|
|`nav`|导航栏|
|`menu`|菜单|
|`article`|文档、内容|
|`aside`|边栏|
|`canvas`|画布（用于绘制图形）|

> 页面中用作链接的按钮应该使用`<a>`, 表单中的按钮使用`<input>`而不是`<button>`

#### 示例
将你构建的页面当作一本书，将标签的语义对应的其功能和含义；

- 书的名称：`<h1>`
- 书的每个章节标题: `<h2>`
- 章节内的文章标题: `<h3>`
- 小标题/副标题: `<h4> <h5> <h6>`
- 章节的段落: `<p>`

> 为SEO考虑，慎用`H1`, `H2`。

更多语义化的内容，参考 sofish 写的文章 [这样去写你的 HTML](http://wenku.baidu.com/view/0a8d3774f242336c1eb95ea9.html)。

### 模块化

html 尽量模块化去写，这样，能提高效率，便于以后维护。
常见模块

- 新闻列表 (news-list)
- 图片列表 (pic-list)
- 排行榜 (rank-list)
- 广告
- 更多...

### HEAD

#### 文档类型

为每个 HTML 页面的第一行添加标准模式（standard mode）的声明， 这样能够确保在每个浏览器中拥有一致的表现。

`<!DOCTYPE html>`

####  语言属性

为什么使用 `lang="zh-cmn-Hans" ` 而不是我们通常写的 lang="zh-CN" 呢? 请参考知乎上的讨论: [网页头部的声明应该是用 lang="zh" 还是 lang="zh-cn"？](http://www.zhihu.com/question/20797118)

```html
<!-- 中文 -->
<html lang="zh-Hans">

<!-- 简体中文 -->
<html lang="zh-cmn-Hans">

<!-- 繁体中文 -->
<html lang="zh-cmn-Hant">

<!-- English -->
<html lang="en">
```

#### meta标签

元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。
标签位于文档的头部，不包含任何内容。 标签的属性定义了与文档相关联的名称/值对。 详细可查看[HTML META 标签](http://www.w3school.com.cn/tags/tag_meta.asp)
常用的meta标签如下, [详情可查看](http://fex.baidu.com/blog/2014/10/html-head-tags/)：

```html
<meta charset="utf-8">
<meta name="renderer" content="webkit">
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
<meta name="keywords" content="your keywords">
<meta name="description" content="your description"> 

以下是移动端用的比较多的
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
<meta name="format-detection"content="telephone=no, email=no" />
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
<meta name="apple-mobile-web-app-capable" content="yes" /><!-- 删除苹果默认的工具栏和菜单栏 -->
<meta name="apple-mobile-web-app-status-bar-style" content="black" /><!-- 设置苹果工具栏颜色 -->
<meta name="format-detection" content="telphone=no, email=no" /><!-- 忽略页面中的数字识别为电话，忽略email识别 -->
<!-- 启用360浏览器的极速模式(webkit) --> 
<!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
<meta name="HandheldFriendly" content="true">
<!-- 微软的老式浏览器 -->
<meta name="MobileOptimized" content="320">
<!-- uc强制竖屏 -->
<meta name="screen-orientation" content="portrait">
<!-- QQ强制竖屏 -->
<meta name="x5-orientation" content="portrait">
<!-- UC强制全屏 -->
<meta name="full-screen" content="yes">
<!-- QQ强制全屏 -->
<meta name="x5-fullscreen" content="true">
<!-- UC应用模式 -->
<meta name="browsermode" content="application">
<!-- QQ应用模式 -->
<meta name="x5-page-mode" content="app">
<!-- windows phone 点击无高光 -->
<meta name="msapplication-tap-highlight" content="no">
<!-- 适应移动端end -->
```

#### 字符编码

- 以无 BOM 的 utf-8 编码作为文件格式;
- 指定字符编码的 meta 必须是 head 的第一个直接子元素；请参考前端观察的博文：[ HTML5 Charset 能用吗？](http://www.qianduan.net/html5-charset-can-it.html)
```html
<html>
  <head>
    <meta charset="utf-8">
    ......
  </head>
  <body>
    ......
  </body>
</html>
```
#### IE 兼容模式

优先使用最新版本的IE 和 Chrome 内核
```html
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
```

#### SEO 优化
```html
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <!-- SEO -->
    <title>Style Guide</title>
    <meta name="keywords" content="your keywords">
    <meta name="description" content="your description">
    <meta name="author" content="author,email address">
</head>
```
#### viewport

- viewport: 一般指的是浏览器窗口内容区的大小，不包含工具条、选项卡等内容；
- width: 浏览器宽度，输出设备中的页面可见区域宽度；
- device-width: 设备分辨率宽度，输出设备的屏幕可见宽度；
- initial-scale: 初始缩放比例；
- maximum-scale: 最大缩放比例；

为移动端设备优化，设置可见区域的宽度和初始缩放比例。

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

#### iOS 图标

apple-touch-icon 图片自动处理成圆角和高光等效果;
apple-touch-icon-precomposed 禁止系统自动添加效果，直接显示设计原图;

```html
<!-- iPhone 和 iTouch，默认 57x57 像素，必须有 -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png">

<!-- iPad，72x72 像素，可以没有，但推荐有 -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-72x72-precomposed.png" sizes="72x72">

<!-- Retina iPhone 和 Retina iTouch，114x114 像素，可以没有，但推荐有 -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-114x114-precomposed.png" sizes="114x114">

<!-- Retina iPad，144x144 像素，可以没有，但推荐有 -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-144x144-precomposed.png" sizes="144x144">
```

#### favicon

在未指定 favicon 时，大多数浏览器会请求 Web Server 根目录下的 favicon.ico 。为了保证 favicon 可访问，避免404，必须遵循以下两种方法之一：

- 在 Web Server 根目录放置 favicon.ico 文件；
- 使用 link 指定 favicon；

```html
<link rel="shortcut icon" href="path/to/favicon.ico">
```

#### HEAD 模板

```html
<!DOCTYPE html>
<html lang="zh-cmn-Hans">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <title>Style Guide</title>
    <meta name="description" content="不超过150个字符">
    <meta name="keywords" content="">
    <meta name="author" content="name, email@gmail.com">

    <!-- 为移动设备添加 viewport -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- iOS 图标 -->
    <link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png">

    <link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml" />
    <link rel="shortcut icon" href="path/to/favicon.ico">
</head>
```
#### 通用模板 

**HTML模板**

html模板如 无特殊需求，都需要采用html5声明 ，即 <!DOCTYPE html>，并且需要加上 兼容的标签 ，以便给客户更好的体验。

- **PC端模板**

```html
<!DOCTYPE html>
<html>
  <head>
      <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>
      <meta charset="utf-8"/>
      <title>页面标题</title>
      <style>
          body,div,form,img,p,h1,h2,dl,dt,dd,ul,li{padding:0;margin:0;}
          ul,li{list-style:none;}
          h3,h4,h5{margin: 0;}
          em{font-style:normal;}
          img{display:block;border:0;}
          a{color:#333;text-decoration:none;}
          a:hover,td a:hover{color:#f60;text-decoration:none;}
          .hong12{color:#fff;}
          .clear{clear:both;display:block;height:0;visibility:hidden;font:0/0 arial;}
          .clearfix:after{content:".";display:block;visibility:hidden;clear:both;height:0;font-size:0;}
          .clearfix{*zoom:1;}
          .d-clear{clear:both}
          .d-clear:after{content: ".";display: block;visibility: hidden;clear: both;height: 0;}
          .d-float-left{float: left;}
          #top{font-size:12px;}
      </style>
  </head>
  <body>
      <div id="top">
          模块内容
      </div>
      <script type="text/javascript">
      </script>   
  </body>
</html>
```
- **移动端模板**
```html
 <!DOCTYPE html>
  <html lang="zh-CN">
  <head>
      <meta charset="UTF-8"/>
      <meta name="HandheldFriendly" content="true" />
      <meta name="MobileOptimized" content="width" />
      <meta name="applicable-device" content="mobile"/>
      <meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" />
      <meta name="keywords" content="" />
      <meta name="description" content="" />
      <!-- 取消iphone 和 andirod 手机默认对页面的信息自动识别功能 -->
      <!-- 电话号码 -->
      <meta name="format-detection" content="telephone=no" />
      <!-- 地址 -->
      <meta name="format-detection" content="address=no" />
      <!-- 电子邮箱 -->
      <meta content="email=no" name="format-detection" />
      <title>
      </title>
  </head>
  <body>
  </body>
</html>
```

## CSS

ascading Style Sheets home page : 里面有关于CSS前生今世的系统的介绍。 [原版地址](http://www.w3.org/Style/CSS/) 、[中文版地址](http://www.webstyles-chinese.info/Style/CSS/)
MDN的学习地址：[CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)

### 通用约定

#### 代码组织

- 以组件为单位组织代码段；
- 制定一致的注释规范；
- 组件块和子组件块以及声明块之间使用一空行分隔，子组件块之间三空行分隔；
如果使用了多个 CSS 文件，将其按照组件而非页面的形式分拆，因为页面会被重组，而组件只会被移动；

良好的注释是非常重要的。请留出时间来描述组件（component）的工作方式、局限性和构建它们的方法。不要让你的团队其它成员 来猜测一段不通用或不明显的代码的目的。

提示：通过配置编辑器，可以提供快捷键来输出一致认可的注释模式。

```css
/* section */
.section{padding: 15px; margin-bottom: 15px;}

/* selector */
.section .selector {padding: 15px; margin-bottom: 15px;} 

/* selector-secondary */
.section .selector-secondary {display: block; /* 注释*/}

.section .selector-three {display: span;}
```

#### Class和ID

- 使用语义化、通用的命名方式；
- 使用连字符 - 作为 ID、Class 名称界定符，不要驼峰命名法和下划线；
- 避免选择器嵌套层级过多，尽量少于 3 级；
- 避免选择器和 Class、ID 叠加使用；

出于[性能考量](http://www.stevesouders.com/blog/2009/06/18/simplifying-css-selectors/)，在没有必要的情况下避免元素选择器叠加 Class、ID 使用。

元素选择器和 ID、Class 混合使用也违反关注分离原则。如果HTML标签修改了，就要再去修改 CSS 代码，不利于后期维护。

```css
/* Not recommended */
.red {}
.box_green {}
.page .header .login #username input {}
ul#example {}

/* Recommended */
#nav {}
.box-video {}
#username input {}
#example {}
```

#### 声明块格式

- 选择器分组时，保持独立的选择器占用一行；
- 声明块的左括号 `{ `前添加一个空格；
- 声明块的右括号 `}` 应单独成行；
- 声明语句中的 `: `后应添加一个空格；
- 声明语句应以分号` ; `结尾；
- 一般以逗号分隔的属性值，每个逗号后应添加一个空格；
- `rgb()、rgba()、hsl()、hsla() `或 `rect() ` 括号内的值，逗号分隔，但逗号后不添加一个空格；
- 对于属性值或颜色参数，省略小于 1 的小数前面的 0 （例如，`.5` 代替 `0.5`；`-.5px `代替 `-0.5px`）；
- 十六进制值应该全部小写和尽量简写，例如，`#fff` 代替 `#ffffff`；
- 避免为 0 值指定单位，例如，用 `margin: 0;` 代替 `margin: 0px;`；
```css
/*  Not recommended  */
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}

/* Recommended */
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin-bottom: 15px;
  background-color: rgba(0,0,0,.5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```

#### 声明顺序

相关属性应为一组，推荐的样式编写顺序

1. Positioning
2. Box model
3. Typographic
4. Visual
由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型决定了组件的尺寸和位置，因此排在第二位。

其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。

```css
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box model */
  display: block;
  box-sizing: border-box;
  width: 100px;
  height: 100px;
  padding: 10px;
  border: 1px solid #e5e5e5;
  border-radius: 3px;
  margin: 10px;
  float: right;
  overflow: hidden;

  /* Typographic */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  text-align: center;

  /* Visual */
  background-color: #f5f5f5;
  color: #fff;
  opacity: .8;

  /* Other */
  cursor: pointer;
}
```

#### 引号使用

`url() `、属性选择符、属性值使用双引号。 参考 [Is quoting the value of url() really necessary?](http://stackoverflow.com/questions/2168855/is-quoting-the-value-of-url-really-necessary)

```css
/* Not recommended */
@import url(//www.google.com/css/maia.css);

html {
  font-family: 'open sans', arial, sans-serif;
}

/* Recommended */
@import url("//www.google.com/css/maia.css");

html {
  font-family: "open sans", arial, sans-serif;
}

.selector[type="text"] {

}
```

#### 媒体查询（Media query）的位置

将媒体查询放在尽可能相关规则的附近。不要将他们打包放在一个单一样式文件中或者放在文档底部。如果你把他们分开了，将来只会被大家遗忘。

```css
.element { ... }
.element-avatar { ... }
.element-selected { ... }

@media (max-width: 768px) {
  .element { ...}
  .element-avatar { ... }
  .element-selected { ... }
}
```

#### 不要使用 `@import`

与 <link> 相比，@import 要慢很多，不光增加额外的请求数，还会导致不可预料的问题。

替代办法：

- 使用多个 元素；
- 通过 Sass 或 Less 类似的 CSS 预处理器将多个 CSS 文件编译为一个文件；
- 其他 CSS 文件合并工具；
- 参考 [don’t use @import](http://www.stevesouders.com/blog/2009/04/09/dont-use-import/)；

#### 链接的样式顺序：

`a:link -> a:visited -> a:hover -> a:active（LoVeHAte）`

#### 无需添加浏览器厂商前缀

使用 [Autoprefixer](https://github.com/postcss/autoprefixer) 自动添加浏览器厂商前缀，编写 CSS 时不需要添加浏览器前缀，直接使用标准的 CSS 编写。

Autoprefixer 通过 [Can I use](http://caniuse.com/)，按兼容的要求，对相应的 CSS 代码添加浏览器厂商前缀。

### 字体排印

暂时参考[网页字体排印指南](http://aaaaaashu.me/shu/)

TODO

### 模块组织

任何超过 1000 行的 CSS 代码，你都曾经历过这样的体验：

1. 这个 class 到底是什么意思呢？
2. 这个 class 在哪里被使用呢？
3. 如果我创建一个 xxoo class，会造成冲突吗？

Reasonable System for CSS Stylesheet Structure 的目标就是解决以上问题，它不是一个框架，而是通过规范，让你构建更健壮和可维护的 CSS 代码。

#### Components（组件）

![Alt text](./1472623451890.png)

从 Components 的角度思考，将网站的模块都作为一个独立的 Components。

**Naming components （组件命名）**

Components **最少以两个单词命名**，通过 - 分离，例如：

- 点赞按钮 (.like-button)
- 搜索框 (.search-form)
- 文章卡片 (.article-card)

#### Elements （元素）
![Alt text](./1472623517640.png)

Elements 是 Components 中的元素

**Naming elements （元素命名）**

Elements 的类名应尽可能仅有一个单词。

```css
.search-form {
    > .field { /* ... */ }
    > .action { /* ... */ }
  }
```

**Avoid tag selectors （避免标签选择器）**

任何时候尽可能使用 classnames。标签选择器在使用上没有问题，但是其性能上稍弱，并且表意不明确。

```css
 .article-card {
    > h3    { /* ✗ avoid */ }
    > .name { /* ✓ better */ }
  }
```

#### Variants （变体）
![Alt text](./1472623633418.png)

Components 和 Elements 可能都会拥有 Variants。

**Naming variants （变体命名）**

Variants 的 classname 应带有前缀中划线 -

```css
  .like-button {
    &.-wide { /* ... */ }
    &.-short { /* ... */ }
    &.-disabled { /* ... */ }
  }
```

**Element variants （元素变体）**

```css
  .shopping-card {
    > .title { /* ... */ }
    > .title.-small { /* ... */ }
  }
```
**Dash prefixes （中划线前缀）**

为什么使用中划线作为变体的前缀？

- 它可以避免歧义与 Elements
- CSS class 仅能以单词和 _ 或 - 开头
- 中划线比下划线更容易输出

#### Layout（布局）

![Alt text](./1472623706917.png)


**Avoid positioning properties （避免定位属性）**

Components 应该在不同的上下文中都可以复用，所以应避免设置以下属性：

- Positioning (position, top, left, right, bottom)
- Floats (float, clear)
- Margins (margin)
- Dimensions (width, height) *

**Fixed dimensions （固定尺寸）**

头像和 logos 这些元素应该设置固定尺寸（宽度，高度...）。

**Define positioning in parents （在父元素中设置定位）**

倘若你需要为组件设置定位，应将在组件的上下文（父元素）中进行处理，比如以下例子中，将 widths 和 floats 应用在 list component(.article-list) 当中，而不是 component(.article-card) 自身。

```css
 .article-list {
    & {
      @include clearfix;
    }

    > .article-card {
      width: 33.3%;
      float: left;
    }
  }

  .article-card {
    & { /* ... */ }
    > .image { /* ... */ }
    > .title { /* ... */ }
    > .category { /* ... */ }
  }
```

#### Avoid over-nesting （避免过分嵌套）

当出现多个嵌套的时候容易失去控制，应保持不超过一个嵌套。

```scss
 /* ✗ Avoid: 3 levels of nesting */
  .image-frame {
    > .description {
      /* ... */

      > .icon {
        /* ... */
      }
    }
  }

  /* ✓ Better: 2 levels */
  .image-frame {
    > .description { /* ... */ }
    > .description > .icon { /* ... */ }
  }
```

#### Apprehensions （顾虑）

- **中划线-是一坨糟糕的玩意**：其实你可以选择性的使用，只要将 Components, Elements, Variants 记在心上即可。
- **我有时候想不出两个单词唉**：有些组件的确使用一个单词就能表意，比如 aleter 。但其实你可以使用后缀，使其意识更加明确。
比如块级元素：
- .alert-box
- .alert-card
- .alert-block
或行内级元素
- .link-button
- .link-span

#### Terminologies （术语）

RSCSS 与其他 CSS 模块组织系统相似的概念

|RSCSS|BEM|SMACSS|
|:----|:----|:----|
|Component|Block|Module|
|Element|Element|?|
|Layout|?|Layout|
|Variant|Modifier|Theme & State|


#### Summary （总结）

- 以 Components 的角度思考，以两个单词命名（.screenshot-image）
- Components 中的 Elements，以一个单词命名（.blog-post .title）
- Variants，以中划线-作为前缀（.shop-banner.-with-icon）
- Components 可以互相嵌套
- 记住，你可以通过继承让事情变得更简单

#### 团队CSS命名规范
##### 常用CSS命名规范
- 头：header
- 内容：content/container
- 尾：footer
- 导航：nav
- 侧栏：sidebar
- 栏目：column
- 页面外围控制整体布局宽度：wrapper
- 左右中：left right center
- 登录条：loginbar
- 标志：logo
- 广告：banner
- 页面主体：main
- 热点：hot
- 新闻：news
- 下载：download
- 子导航：subnav
- 菜单：menu
- 子菜单：submenu
- 搜索：search
- 友情链接：friendlink
- 页脚：footer
- 版权：copyright
- 滚动：scroll
- 内容：content
- 标签页：tab
- 文章列表：list
- 提示信息：msg
- 小技巧：tips
- 栏目标题：title
- 加入：joinus
- 指南：guide
- 服务：service
- 注册：register
- 状态：status
- 投票：vote
- 合作伙伴：partner

注释的写法：

```css
/* Footer */
内容区
/* End Footer */
```

##### id的命名：
1. 页面结构
  - 容器: container
  - 页头:header
  - 内容: content/container
  - 页面主体: main
  - 页尾: footer
  - 导航: nav
  - 侧栏: sidebar
  - 栏目: column
  - 页面外围控制整体布局宽度: wrapper
  - 左右中: left right center
2. 导航
  - 导航: nav
  - 主导航: mainnav
  - 子导航: subnav
  - 顶导航: topnav
  - 边导航: sidebar
  - 左导航: leftsidebar
  - 右导航: rightsidebar
  - 菜单: menu
  - 子菜单: submenu
  - 标题: title
  - 摘要: summary
3. 功能
  -  标志: logo
  - 广告: banner
  - 登陆: login
  - 登录条: loginbar
  - 注册: regsiter
  - 搜索: search
  - 功能区: shop
  - 标题: title
  - 加入: joinus
  - 状态: status
  - 按钮: btn
  - 滚动: scroll
  - 标签页: tab
  - 文章列表: list
  - 提示信息: msg
  - 当前的: current
  - 小技巧: tips
  - 图标: icon
  - 注释: note
  - 指南: guide
  - 服务: service
  - 热点: hot
  - 新闻: news
  - 下载: download
  - 投票: vote
  - 合作伙伴: partner
  - 友情链接: link
  - 版权: copyright

##### class的命名：
1. 颜色:使用颜色的名称或者16进制代码,如
  - .red { color: red; }
  - .f60 { color: #f60; }
  - .ff8600 { color: #ff8600; }
2. 字体大小,直接使用”font+字体大小”作为名称,如
  - .font12px { font-size: 12px; }
  - .font9pt {font-size: 9pt; }
3. 对齐样式,使用对齐目标的英文名称,如
  - .left { float:left; }
  - .bottom { float:bottom; }
4. 标题栏样式,使用”类别+功能”的方式命名,如
  - .barnews { }
  - .barproduct { }
**注意事项:**
1. 一律小写;
2. 尽量用英文;
3. 不加中杠和下划线;
4. 尽量不缩写，除非一看就明白的单词.
  - 主要的 master.css
  - 模块 module.css
  - 基本共用 base.css
  - 布局，版面 layout.css
  - 主题 themes.css
  - 专栏 columns.css
  - 文字 font.css
  - 表单 forms.css
  - 补丁 mend.css
  - 打印 print.css

### LESS/SASS

#### 代码组织

代码按一下顺序组织：

1. @import
2. 变量声明
3. 样式声明
```scss
@import "mixins/size.scss";

@default-text-color: #333;

.page {
  width: 960px;
  margin: 0 auto;
}
```

#### @import 语句

@import 语句引用的文需要写在一对引号内，.scss 后缀不得省略。引号使用 ' 和 " 均可，但在同一项目内需统一。
```scss
/* Not recommended */
@import "mixins/size";
@import 'mixins/grid.scss';

/* Recommended */
@import "mixins/size.scss";
@import "mixins/grid.scss";
```

#### 混入（Mixin）

1. 在定义 mixin 时，如果 mixin 名称不是一个需要使用的 className，必须加上括号，否则即使不被调用也会输出到 CSS 中。

2. 如果混入的是本身不输出内容的 mixin，需要在 mixin 后添加括号（即使不传参数），以区分这是否是一个 className。
```scss
/* Not recommended */
.big-text {
  font-size: 2em;
}

h3 {
  .big-text;
  .clearfix;
}

/* Recommended */
.big-text() {
  font-size: 2em;
}

h3 {
  .big-text(); /* 1 */
  .clearfix(); /* 2 */
}
```

#### 避免嵌套层级过多

- 将嵌套深度限制在2级。对于超过3级的嵌套，给予重新评估。这可以避免出现过于详实的CSS选择器。
- 避免大量的嵌套规则。当可读性受到影响时，将之打断。推荐避免出现多于20行的嵌套规则出现。

#### 字符串插值

变量可以用类似ruby和php的方式嵌入到字符串中，像@{name}这样的结构: `@base-url: "http://assets.fnord.com"; background-image: url("@{base-url}/images/bg.png");`

### 性能优化
#### 慎重选择高消耗的样式

高消耗属性在绘制前需要浏览器进行大量计算：

- box-shadows
- border-radius
- transparency
- transforms
- CSS filters（性能杀手）

#### 避免过分重排

当发生重排的时候，浏览器需要重新计算布局位置与大小，[更多详情](http://www.jianshu.com/p/e305ace24ddf)。

常见的重排元素:

- width
- height
- padding
- margin
- display
- border-width
- position
- top
- left
- right
- bottom
- font-size
- float
- text-align
- overflow-y
- font-weight
- overflow
- font-family
- line-height
- vertical-align
- clear
- white-space
- min-height

#### 正确使用 Display 的属性

Display 属性会影响页面的渲染，请合理使用。

- display: inline后不应该再使用 width、height、margin、padding 以及 float；

- display: inline-block 后不应该再使用 float；

- display: block 后不应该再使用 vertical-align；

- display: table-* 后不应该再使用 margin 或者 float；

#### 不滥用 Float

Float在渲染时计算量比较大，尽量减少使用。


#### 动画性能优化

动画的实现原理，是利用了人眼的“视觉暂留”现象，在短时间内连续播放数幅静止的画面，使肉眼因视觉残象产生错觉，而误以为画面在“动”。

动画的基本概念：

- 帧：在动画过程中，每一幅静止画面即为一“帧”;
- 帧率：即每秒钟播放的静止画面的数量，单位是fps(Frame per second);
- 帧时长：即每一幅静止画面的停留时间，单位一般是ms(毫秒);
- 跳帧(掉帧/丢帧)：在帧率固定的动画中，某一帧的时长远高于平均帧时长，导致其后续数帧被挤压而丢失的现象。
一般浏览器的渲染刷新频率是 60 fps，所以在网页当中，帧率如果达到 50-60 fps 的动画将会相当流畅，让人感到舒适。

- 如果使用基于 javaScript 的动画，尽量使用 requestAnimationFrame. 避免使用 setTimeout, setInterval.
- 避免通过类似 jQuery animate()-style 改变每帧的样式，使用 CSS 声明动画会得到更好的浏览器优化。
- 使用 translate 取代 absolute 定位就会得到更好的 fps，动画会更顺滑。

![Alt text](./1472627798786.png)


#### 多利用硬件能力，如通过 3D 变形开启 GPU 加速

一般在 Chrome 中，3D或透视变换（perspective transform）CSS属性和对 opacity 进行 CSS 动画会创建新的图层，在硬件加速渲染通道的优化下，GPU 完成 3D 变形等操作后，将图层进行复合操作（Compesite Layers），从而避免触发浏览器大面积重绘和重排。

注：3D 变形会消耗更多的内存和功耗。

使用 translate3d 右移 500px 的动画流畅度要明显优于直接使用 left：

```scss
.ball-1 {
  transition: -webkit-transform .5s ease;
  -webkit-transform: translate3d(0, 0, 0);
}
.ball-1.slidein{
  -webkit-transform: translate3d(500px, 0, 0);
}
.ball-2 {
  transition: left .5s ease; left：0;
}
.ball-2.slidein {
  left：500px;
}
```

#### 提升 CSS 选择器性能

CSS 选择器对性能的影响源于浏览器匹配选择器和文档元素时所消耗的时间，所以优化选择器的原则是应尽量避免使用消耗更多匹配时间的选择器。而在这之前我们需要了解 CSS 选择器匹配的机制， 如子选择器规则：

```scss
#header > a {font-weight:blod;}
```

我们中的大多数人都是从左到右的阅读习惯，会习惯性的设定浏览器也是从左到右的方式进行匹配规则，推测这条规则的开销并不高。

我们会假设浏览器以这样的方式工作：寻找 id 为 header 的元素，然后将样式规则应用到直系子元素中的 a 元素上。我们知道文档中只有一个 id 为 header 的元素，并且它只有几个 a 元素的子节点，所以这个 CSS 选择器应该相当高效。

事实上，却恰恰相反，CSS 选择器是从右到左进行规则匹配。了解这个机制后，例子中看似高效的选择器在实际中的匹配开销是很高的，浏览器必须遍历页面中所有的 a 元素并且确定其父元素的 id 是否为 header 。

如果把例子的子选择器改为后代选择器则会开销更多，在遍历页面中所有 a 元素后还需向其上级遍历直到根节点。

```scss
#header  a {font-weight:blod;}
```

理解了CSS选择器从右到左匹配的机制后，明白只要当前选择符的左边还有其他选择符，样式系统就会继续向左移动，直到找到和规则匹配的选择符，或者因为不匹配而退出。我们把最右边选择符称之为关键选择器。——[更多详情](http://www.jianshu.com/p/268c7f3dd7a6)

1. 避免使用通用选择期

```scss
/* Not recommended */
.content * {color: red;}
```

浏览器匹配文档中所有的元素后分别向上逐级匹配 class 为 content 的元素，直到文档的根节点。因此其匹配开销是非常大的，所以应避免使用关键选择器是通配选择器的情况。

2. 避免使用标签或 class 选择器限制 id 选择器
```scss
/* Not recommended */
button#backButton {…}
/* Recommended */
#newMenuIcon {…}
```
3. 避免使用标签限制 class 选择器
```scss
/* Not recommended */
treecell.indented {…}
/* Recommended */
.treecell-indented {…}
/* Much to recommended */
.hierarchy-deep {…}
```
4. 避免使用多层标签选择器。使用 class 选择器替换，减少css查找
```scss
/* Not recommended */
treeitem[mailfolder="true"] > treerow > treecell {…}
/* Recommended */
.treecell-mailfolder {…}
```
5. 避免使用子选择器
```scss
/* Not recommended */
treehead treerow treecell {…}
/* Recommended */
treehead > treerow > treecell {…}
/* Much to recommended */
.treecell-header {…}
```
6. 使用继承
```scss
/* Not recommended */
#bookmarkMenuItem > .menu-left { list-style-image: url(blah) }
/* Recommended */
#bookmarkMenuItem { list-style-image: url(blah) }
```

## Javascript

### 通用约定

#### 注释

**原则**

As short as possible（如无必要，勿增注释）：尽量提高代码本身的清晰性、可读性。
As long as necessary（如有必要，尽量详尽）：合理的注释、空行排版等，可以让代码更易阅读、更具美感。

**单行注释**
必须独占一行。`//` 后跟一个空格，缩进与下一行被注释说明的代码一致。

**多行注释**

避免使用` /*...*/` 这样的多行注释。有多行注释内容时，使用多个单行注释。

**函数/方法注释**

1. 函数/方法注释必须包含函数说明，有参数和返回值时必须使用注释标识。；
2. 参数和返回值注释必须包含类型信息和说明；
3. 当函数是内部函数，外部不可访问时，可以使用 @inner 标识；

```javascript
/**
 * 函数描述
 *
 * @param {string} p1 参数1的说明
 * @param {string} p2 参数2的说明，比较长
 *     那就换行了.
 * @param {number=} p3 参数3的说明（可选）
 * @return {Object} 返回值描述
 */
function foo(p1, p2, p3) {
    var p3 = p3 || 10;
    return {
        p1: p1,
        p2: p2,
        p3: p3
    };
}
```

**文件注释**

文件注释用于告诉不熟悉这段代码的读者这个文件中包含哪些东西。 应该提供文件的大体内容, 它的作者, 依赖关系和兼容性信息。如下:

```javascript
/**
 * @fileoverview Description of file, its uses and information
 * about its dependencies.
 * @author user@meizu.com (Firstname Lastname)
 * Copyright 2009 Meizu Inc. All Rights Reserved.
 */
```

#### 命名

**变量,** 使用 Camel 命名法。
```javascript
var loadingModules = {};
```

**私有属性、变量和方法**以下划线 _ 开头。
```javascript
var _privateMethod = {};
```

**常量**, 使用全部字母大写，单词间下划线分隔的命名方式。
```javascript
var HTML_ENTITY = {};
```

1. **函数**, 使用 Camel 命名法。
2, 函数的**参数**, 使用 Camel 命名法。

```javascript
function stringFormat(source) {}

function hear(theBells) {}
```

1. **类**, 使用 Pascal 命名法
2. 类的 **方法 / 属性**, 使用 Camel 命名法

```javascript
function TextNode(value, engine) {
    this.value = value;
    this.engine = engine;
}

TextNode.prototype.clone = function () {
    return this;
};
```

1. **枚举变量** 使用 Pascal 命名法。
2. **枚举的属性**， 使用全部字母大写，单词间下划线分隔的命名方式。

```javascript
var TargetState = {
    READING: 1,
    READED: 2,
    APPLIED: 3,
    READY: 4
};
```

由多个单词组成的 **缩写词**，在命名中，根据当前命名法和出现的位置，所有字母的大小写与首字母的大小写保持一致。
```javascript
function XMLParser() {}

function insertHTML(element, html) {}

var httpRequest = new HTTPRequest();
```

#### 命名语法

**类名**，使用名词。
```javascript
function Engine(options) {}
```

**函数名**，使用动宾短语。
```javascript
function getStyle(element) {}
```

**boolean** 类型的变量使用 is 或 has 开头。
```javascript
var isReady = false;
var hasMoreCommands = false;
```

**Promise 对象**用动宾短语的进行时表达。
```javascript
var loadingData = ajax.get('url');
loadingData.then(callback);
```

#### 接口命名规范

1. 可读性强，见名晓义；
2. 尽量不与 jQuery 社区已有的习惯冲突；
3. 尽量写全。不用缩写，除非是下面列表中约定的；（变量以表达清楚为目标，uglify 会完成压缩体积工作

|常用词|说明|
|:----|:----|
|options|表示选项，与 jQuery 社区保持一致，不要用 config, opts 等|
|active|  表示当前，不要用 current 等|
|index| 表示索引，不要用 idx 等|
|trigger| 触点元素|
|triggerType| 触发类型、方式|
|context| 表示传入的 this 对象|
|object|  推荐写全，不推荐简写为 o, obj 等|
|element| 推荐写全，不推荐简写为 el, elem 等|
|length | 不要写成 len, l|
|prev | previous 的缩写|
|next|  next 下一个|
|constructor| 不能写成 ctor|
|easing|  示动画平滑函数|
|min| minimize 的缩写|
|max  |maximize 的缩写|
|DOM  |不要写成 dom, Dom|
|.hbs |使用 hbs 后缀表示模版|
|btn  |button 的缩写|
|link |超链接|
|title  |主要文本|
|img  |图片路径（img标签src属性）|
|dataset  | html5 data-xxx 数据接口|
|theme| 主题|
|className  |类名|
|classNameSpace | class 命名空间|

#### True 和 False 布尔表达式

类型检测优先使用 typeof。对象类型检测使用 instanceof。null 或 undefined 的检测使用 == null。

下面的布尔表达式都返回 false:

- null
- undefined
- '' 空字符串
- 0 数字0

但小心下面的, 可都返回 true:

- '0' 字符串0
- [] 空数组
- {} 空对象

#### 不要在 Array 上使用 for-in 循环

for-in 循环只用于 object/map/hash 的遍历, 对 Array 用 for-in 循环有时会出错. 因为它并不是从 0 到 length - 1 进行遍历, 而是所有出现在对象及其原型链的键值。
```javasript
// Not recommended
function printArray(arr) {
  for (var key in arr) {
    print(arr[key]);
  }
}

printArray([0,1,2,3]);  // This works.

var a = new Array(10);
printArray(a);  // This is wrong.

a = document.getElementsByTagName('*');
printArray(a);  // This is wrong.

a = [0,1,2,3];
a.buhu = 'wine';
printArray(a);  // This is wrong again.

a = new Array;
a[3] = 3;
printArray(a);  // This is wrong again.

// Recommended
function printArray(arr) {
  var l = arr.length;
  for (var i = 0; i < l; i++) {
    print(arr[i]);
  }
}
```

#### 二元和三元操作符

操作符始终写在前一行, 以免分号的隐式插入产生预想不到的问题。
```javascript
var x = a ? b : c;

var y = a ?
    longButSimpleOperandB : longButSimpleOperandC;

var z = a ?
        moreComplicatedB :
        moreComplicatedC;
. 操作符也是如此：

var x = foo.bar().
    doSomething().
    doSomethingElse();
```

#### 条件(三元)操作符 (?:)

三元操作符用于替代 if 条件判断语句。

```javascript
// Not recommended
if (val != 0) {
  return foo();
} else {
  return bar();
}

// Recommended
return val ? foo() : bar();
```

#### && 和 ||

二元布尔操作符是可短路的, 只有在必要时才会计算到最后一项。
```javascript
// Not recommended
function foo(opt_win) {
  var win;
  if (opt_win) {
    win = opt_win;
  } else {
    win = window;
  }
  // ...
}

if (node) {
  if (node.kids) {
    if (node.kids[index]) {
      foo(node.kids[index]);
    }
  }
}

// Recommended
function foo(opt_win) {
  var win = opt_win || window;
  // ...
}

var kid = node && node.kids && node.kids[index];
if (kid) {
  foo(kid);
}
```

### jQuery 规范

#### 使用最新版本的jQuery
最新版本的 jQuery 会改进性能和增加新功能，若不是为了兼容旧浏览器，建议使用最新版本的 jQuery。以下是三条常见的 jQuery 语句，版本越新，性能越好：
```javascript
$('.elem')
$('.elem', context)
context.find('.elem')
```

#### jQuery 变量

1. 存放 jQuery 对象的变量以 `$` 开头；
2. 将 jQuery 选择器返回的对象缓存到本地变量中复用；
3. 使用驼峰命名变量；
```javascript
var $myDiv = $("#myDiv");
$myDiv.click(function(){...});
```

#### 选择器

1. 尽可能的使用 ID 选择器，因为它会调用浏览器原生方法 document.getElementById 查找元素。当然直接使用原生 document.getElementById 方法性能会更好；
2. 在父元素中选择子元素使用 .find() 方法性能会更好, 因为 ID 选择器没有使用到 Sizzle 选择器引擎来查找元素；

```javascript
// Not recommended
var $productIds = $("#products .class");

// Recommended
var $productIds = $("#products").find(".class");
```


#### DOM 操作

1. 当要操作 DOM 元素的时候，尽量将其分离节点，操作结束后，再插入节点；
2. 使用字符串连接或 `array.join` 要比 `.append()` 性能更好；

```javascript
var $myList = $("#list-container > ul").detach();
//...a lot of complicated things on $myList
$myList.appendTo("#list-container");
```

```javascript
// Not recommended
var $myList = $("#list");
for(var i = 0; i < 10000; i++){
    $myList.append("<li>"+i+"</li>");
}

// Recommended
var $myList = $("#list");
var list = "";
for(var i = 0; i < 10000; i++){
    list += "<li>"+i+"</li>";
}
$myList.html(list);

// Much to recommended
var array = [];
for(var i = 0; i < 10000; i++){
    array[i] = "<li>"+i+"</li>";
}
$myList.html(array.join(''));
```

#### 事件

1. 如果需要，对事件使用自定义的 namespace，这样容易解绑特定的事件，而不会影响到此 DOM 元素的其他事件监听；
2. 对 Ajax 加载的 DOM 元素绑定事件时尽量使用事件委托。事件委托允许在父元素绑定事件，子代元素可以响应事件，也包括 Ajax 加载后添加的子代元素；

```javascript
$("#myLink").on("click.mySpecialClick", myEventHandler);
$("#myLink").unbind("click.mySpecialClick");
```

```javascript

// Not recommended
$("#list a").on("click", myClickHandler);

// Recommended
$("#list").on("click", "a", myClickHandler);
```


#### 链式写法

1. 尽量使用链式写法而不是用变量缓存或者多次调用选择器方法；
2. 当链式写法超过三次或者因为事件绑定变得复杂后，使用换行和缩进保持代码可读性；

```javascript
$("#myDiv").addClass("error").show();
```
```javascript
$("#myLink")
  .addClass("bold")
  .on("click", myClickHandler)
  .on("mouseover", myMouseOverHandler)
  .show();
```

#### 其他

1. 多个参数使用对象字面量存储；
2. 不要将 CSS 写在 jQuery 里面；
3. 正则表达式仅准用 .test() 和 .exec() 。不准用 "string".match() ；


#### jQuery 插件模板

```javascript
// jQuery Plugin Boilerplate
// A boilerplate for jumpstarting jQuery plugins development
// version 1.1, May 14th, 2011
// by Stefan Gabos

// remember to change every instance of "pluginName" to the name of your plugin!
(function($) {

    // here we go!
    $.pluginName = function(element, options) {

        // plugin's default options
        // this is private property and is  accessible only from inside the plugin
        var defaults = {

            foo: 'bar',

            // if your plugin is event-driven, you may provide callback capabilities
            // for its events. execute these functions before or after events of your
            // plugin, so that users may customize those particular events without
            // changing the plugin's code
            onFoo: function() {}

        }

        // to avoid confusions, use "plugin" to reference the
        // current instance of the object
        var plugin = this;

        // this will hold the merged default, and user-provided options
        // plugin's properties will be available through this object like:
        // plugin.settings.propertyName from inside the plugin or
        // element.data('pluginName').settings.propertyName from outside the plugin,
        // where "element" is the element the plugin is attached to;
        plugin.settings = {}

        var $element = $(element), // reference to the jQuery version of DOM element
             element = element;    // reference to the actual DOM element

        // the "constructor" method that gets called when the object is created
        plugin.init = function() {

            // the plugin's final properties are the merged default and
            // user-provided options (if any)
            plugin.settings = $.extend({}, defaults, options);

            // code goes here

        }

        // public methods
        // these methods can be called like:
        // plugin.methodName(arg1, arg2, ... argn) from inside the plugin or
        // element.data('pluginName').publicMethod(arg1, arg2, ... argn) from outside
        // the plugin, where "element" is the element the plugin is attached to;

        // a public method. for demonstration purposes only - remove it!
        plugin.foo_public_method = function() {

            // code goes here

        }

        // private methods
        // these methods can be called only from inside the plugin like:
        // methodName(arg1, arg2, ... argn)

        // a private method. for demonstration purposes only - remove it!
        var foo_private_method = function() {

            // code goes here

        }

        // fire up the plugin!
        // call the "constructor" method
        plugin.init();

    }

    // add the plugin to the jQuery.fn object
    $.fn.pluginName = function(options) {

        // iterate through the DOM elements we are attaching the plugin to
        return this.each(function() {

            // if plugin has not already been attached to the element
            if (undefined == $(this).data('pluginName')) {

                // create a new instance of the plugin
                // pass the DOM element and the user-provided options as arguments
                var plugin = new $.pluginName(this, options);

                // in the jQuery version of the element
                // store a reference to the plugin object
                // you can later access the plugin and its methods and properties like
                // element.data('pluginName').publicMethod(arg1, arg2, ... argn) or
                // element.data('pluginName').settings.propertyName
                $(this).data('pluginName', plugin);

            }

        });

    }

})(jQuery);
```

此 jQuery 插件模板出自：[jQuery Plugin Boilerplate, revisited](http://stefangabos.ro/jquery/jquery-plugin-boilerplate-revisited/)

### 性能优化

#### 避免不必要的 DOM 操作

浏览器遍历 DOM 元素的代价是昂贵的。最简单优化 DOM 树查询的方案是，当一个元素出现多次时，将它保存在一个变量中，就避免多次查询 DOM 树了。

```javascript
// Recommended
var myList = "";
var myListHTML = document.getElementById("myList").innerHTML;

for (var i = 0; i < 100; i++) {
  myList += "<span>" + i + "</span>";
}

myListHTML = myList;

// Not recommended
for (var i = 0; i < 100; i++) {
  document.getElementById("myList").innerHTML += "<span>" + i + "</span>";
}
```
#### 缓存数组长度

循环无疑是和 JavaScript 性能非常相关的一部分。通过存储数组的长度，可以有效避免每次循环重新计算。

注: 虽然现代浏览器引擎会自动优化这个过程，但是不要忘记还有旧的浏览器。

```javascript
var arr = new Array(1000),
    len, i;
// Recommended - size is calculated only 1 time and then stored
for (i = 0, len = arr.length; i < len; i++) {

}

// Not recommended - size needs to be recalculated 1000 times
for (i = 0; i < arr.length; i++) {

}
```

#### 异步加载第三方内容

当你无法保证嵌入第三方内容比如 Youtube 视频或者一个 like/tweet 按钮可以正常工作的时候，你需要考虑用异步加载这些代码，避免阻塞整个页面加载。

```javascript
(function() {

    var script,
        scripts = document.getElementsByTagName('script')[0];

    function load(url) {
      script = document.createElement('script');
      script.async = true;
      script.src = url;
      scripts.parentNode.insertBefore(script, scripts);
    }

    load('//apis.google.com/js/plusone.js');
    load('//platform.twitter.com/widgets.js');
    load('//s.widgetsite.com/widget.js');

}());
```

#### 避免使用 jQuery 实现动画

1. 禁止使用 `slideUp/Down() fadeIn/fadeOut()` 等方法；
2. 尽量不使用 `animate()` 方法；

## 移动端

移动终端或者叫移动通信终端是指可以在移动中使用的计算机设备，广义的讲包括手机、笔记本、平板电脑、POS机甚至包括车载电脑。但是大部分情况下是指手机或者具有多种应用功能的智能手机以及平板电脑。
随着网络和技术朝着越来越宽带化的方向的发展，移动通信产业将走向真正的移动信息时代。
随着集成电路技术的飞速发展，移动终端的处理能力已经拥有了强大的处理能力，移动终端正在从简单的通话工具变为一个综合信息处理平台。

### 通用规则

- WAP/WAP 1.1 由于许多手机浏览器不支持 CSS、背景图片，所以需要保证为 WAP 开发的网页在没有 CSS 的情况下的可用性。 许多浏览器（包括 MTK 手机）也不支持 card、go 等 WML 标签，多数情况下应采用 HTML 的格式。
- WAP 2.0 WAP 2.0 Profile 是 XHTML1.1 版本，适用大部分 XHTML 规范。为 WAP 2.0 Profile 编写网页时请遵守前面为 PC Web 定义的规范。
- Viewport（webkit） 在 head 标签内添加 viewport 的 meta 来定义 viewport 大小、是否允许缩放等： `<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />`
- HTML（webkit） 为 Webkit 浏览器编写网页时，请尽量使用 HTML5 来实现。 不可使用 frameset/iframe；不可使用` <input type="file" />`；合理利用 placeholder 等特有功能；合理利用 video/canvas 等新标签。
- 图片 --- 双倍图片 由于 Android 1.6 和 iOS 5 能够使用多种屏幕像素密度来表现图像，因此在移动客户端设备的的图片需要考虑至少两种的 DPI 对图片的影响。

> 举例来说，iPhone 4 的屏幕分辨率是 640x960，但是在显示网页或应用时，是使用 4 个物理像素来显示一个点，以此达到精致细腻的卓越显示效果。实际上我们需要提供的是 320 像素的内容。
> 在此时显示一张 100x75 的图片，由于实际渲染了 200x150 的屏幕区域，而所有硬件图形处理器都会使用简单的线性过渡而不是临近像素的方案来放大图片，因此我们会发现图片在网页中看起来模糊，不够细腻。 为了达到细腻的效果，我们需要提供一张 200x150 的图片，然后定义它的尺寸为 100x75，例如`<img src=”images/product-200x150.png” alt=”” />` 在背景中使用此种方式时，可以使用 background-size: 100px 75px 来定义背景图片的大小。

- 使用 CSS3 和内容生成技术来代替常用的按钮、旗帜、箭头、图标，这样可以不用考虑高 DPI 引起的图像模糊问题，并能提高页面载入性能，减少用户付费流量消耗。

> 以下是一些简单的实例：
> 关于如何使用 CSS3 和内容生成技术，请参考： http://nicolasgallagher.com/pure-css-gui-icons/
> 为简单网页中的像素图片、尺寸极小的图片使用 BASE64 方式载入可以减少 HTTP 请求，节约无线网络连接。因为创建无线网络连接需要消耗大量的时间。 下面是 BASE64 图片的使用示例： `<img src=”data:image/png;base64,iVBOw0ABh...” />` .entity { background: url(data:image/png;base64,iVBOw0ABh...) x-repeat 0 0; } 关于图片转 BASE64 编码请参考：http://www.pjhome.net/web/html5/encodeDataUrl.htm

- CSS（webkit） wap端由于设备等原因影响和PC端有一些区别：
  - 不需要添加:hover效果；
  - 不需要添加cursor效果；
  - 表单对象通常有默认的border-image，如果需要自定义表单对象外观，可以使用样式 border:0 none; border-image:none 来去除border-image 的影响；或者使用-webkit-appearance属性更改默认表现样式；
  - 使用 CSS 无法区分 iPhone 和 Android；如要求特别，可以为高 DPI 的屏幕（如 480*800 的 Android 手机和 iPhone4/S 等）提供高分辨率的背景图，然后使用-webkit-background-sizing来约束大小；
  - Android 手机使用圆角边框画出的圆圈锯齿较为严重，如果要求严格，请考虑使用图片实现（此种情况在安卓2.2以下显示明显，现在几乎可以忽略不计）；
  - Android 的 display: none 和 z-index 存在 BUG，有时你可以触摸到隐藏在后面的 Element；因此，应尽量避免使用 position 样式，特别是不要在表单元素上使用。

- 脚本组件和框架（webkit） 由于 Webkit 已经实现了大部分框架功能，同时基本上无须考虑跨浏览器兼容性，所以尽量不要使用 jQueryMobile 等大型框架。
- 新的脚本功能和关键词（webkit）
  - 自带选择器：document.querySelector/querySelectorAll；
  - 复制 DOM 对象：Element.cloneNode；
  - 多数常用的 prototype 已被实现，例如 Array.forEach, Array.indexOf, Array.lastIndexof, String.trim, String.trimLeft, String.trimRight等；
  - 如果需要调试，可以使用 iOS 设备上 Safari 的调试模式；
  - 三星手机的浏览器获取 DOM 的 innerHTML 对其中的相对路径处理不一样，在 使用innerHTML作为模版的场景需要特别处理。

### 移动端优化

#### click 的 300ms 延迟响应

click 的 300ms 延迟是由双击缩放(double tap to zoom)所导致的，由于用户可以进行双击缩放或者双击滚动的操作，当用户一次点击屏幕之后，浏览器并不能立刻判断用户是确实要打开这个链接，还是想要进行双击操作。因此，移动端浏览器就等待 300 毫秒，以判断用户是否再次点击了屏幕。

随着响应式网页逐渐增多，用户使用双击缩放机会减少，这 300ms 的延迟就更不可接受了。浏览器开发商也随之提供相应的解决方案。这些方案在[5 Ways to Prevent the 300ms Click Delay on Mobile Devices](http://www.sitepoint.com/5-ways-prevent-300ms-click-delay-mobile-devices/) 中，被提及的包括「禁用缩放」和「width=device-width」等方案，但这些方案并不完美，需要针对某些版本浏览器，又或仅在 Android 的浏览器上使用。

所以这时候就需要一个更简单通用的解决方案，其中 [FT Labs](http://labs.ft.com/) 专门为解决移动端浏览器 300 毫秒点击延迟问题所开发的一个轻量级的库 FastClick 就是很好的选择。[FastClick](https://github.com/ftlabs/fastclick) 在检测到 touchend 事件的时候，会通过 DOM 自定义事件立即触发一个模拟 click 事件，并把浏览器在 300 毫秒之后真正触发的 click 事件阻止掉。

FastClick 的使用方法非常简单，在 window load 事件之后，在 <body> 上调用`FastClick.attach()` 即可。

```javascript
window.addEventListener( "load", function() {
    FastClick.attach( document.body );
}, false );
```

#### 快速回弹滚动

快速回弹滚动在手机浏览器上的发展历史：

1. 早期的时候，移动端的浏览器都不支持非 body 元素的滚动条，所以一般都借助 iScroll;
2. Android 3.0 / iOS 解决了非 body 元素的滚动问题，但滚动条不可见，同时 iOS 上只能通过2个手指进行滚动；
3. Android 4.0 解决了滚动条不可见及增加了快速回弹滚动效果，不过随后这个特性又被移除；
4. iOS从5.0开始解决了滚动条不可见及增加了快速回弹滚动效果
如果想要为某个元素拥有 Native 般的滚动效果，可以这样操作：

```javascript
.element {
    overflow: auto; /* auto | scroll */
    -webkit-overflow-scrolling: touch;
}
```

除了 iScroll 之外，还有一个更加强大的滚动插件 [Swiper](http://www.idangero.us/swiper/#.VfaVk52qqko)，支持 3D 和内置滚动条等。

#### 设备检测

```javascript
// 这段代码引用自：https://github.com/binnng/device.js

var WIN = window;
var LOC = WIN["location"];
var NA = WIN.navigator;
var UA = NA.userAgent.toLowerCase();

function test(needle) {
  return needle.test(UA);
}

var IsTouch = "ontouchend" in WIN;
var IsAndroid = test(/android|htc/) || /linux/i.test(NA.platform + "");
var IsIPad = !IsAndroid && test(/ipad/);
var IsIPhone = !IsAndroid && test(/ipod|iphone/);
var IsIOS = IsIPad || IsIPhone;
var IsWinPhone = test(/windows phone/);
var IsWebapp = !!NA["standalone"];
var IsXiaoMi = IsAndroid && test(/mi\s+/);
var IsUC = test(/ucbrowser/);
var IsWeixin = test(/micromessenger/);
var IsBaiduBrowser = test(/baidubrowser/);
var IsChrome = !!WIN["chrome"];
var IsBaiduBox = test(/baiduboxapp/);
var IsPC = !IsAndroid && !IsIOS && !IsWinPhone;
var IsHTC = IsAndroid && test(/htc\s+/);
var IsBaiduWallet = test(/baiduwallet/);
```

#### 获取滚动条值

PC 端滚动条的值是通过 document.scrollTop 和 document.scrollLeft 获得，但在 iOS 中并没有滚动条的概念，所以仅能通过 windows.scroll 获取，同时也能兼容 Android 。

```javascript
window.scrollY
window.scrollX
```
#### 清除输入框内阴影

在 iOS 上，输入框默认有内部阴影，但无法使用 box-shadow 来清除，如果不需要阴影，可以这样操作：

```scss
input,
textarea {
    border: 0; /* 方法1 */
    -webkit-appearance: none; /* 方法2 */
}
```

#### Meta 相关

**页面窗口自动调整到设备宽度，并禁止用户缩放页面**

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no" />
```

**电话号码识别**

iOS Safari ( Android 或其他浏览器不会) 会自动识别看起来像电话号码的数字，将其处理为电话号码链接，比如：

- 7位数字，形如：1234567
- 带括号及加号的数字，形如：(+86)123456789
- 双连接线的数字，形如：00-00-00111
- 11位数字，形如：13800138000

```html
<!-- 关闭电话号码识别： -->
<meta name="format-detection" content="telephone=no" />

<!-- 开启电话功能： -->
<a href="tel:123456">123456</a>

<!-- 开启短信功能： -->
<a href="sms:123456">123456</a>
```

**邮箱地址的识别**

在 Android （ iOS 不会）上，浏览器会自动识别看起来像邮箱地址的字符串，不论有你没有加上邮箱链接，当你在这个字符串上长按，会弹出发邮件的提示。

```html
<!-- 关闭邮箱地址识别： -->
<meta name="format-detection" content="email=no" />

<!-- 开启邮件发送： -->
<a mailto:>mobile@gmail.com">mobile@gmail.com</a>
```

**指定 iOS 的 safari 顶端状态条的样式**
```html
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
<!-- 可选default、black、black-translucent -->
```

### 移动端适配

现在手机屏幕是越来越大，各种分辨率也越来越多。从2010年的iPhone 4，到2015年的iPhone 6 plus，从小米1到现在的小米 note3... 每年都会有新的手机出现，而且手机屏幕也越来越杂乱。我们的wap站需要尽量适配更多手机；更有甚者，某些情况下横竖屏切换时都要适配。为了节约成本和时间，移动端适配显得越来越重要。
那么应该如何去做才能实现呢？这是我们需要思考的问题。
移动端适配，暂时分两种情况：

暂时以640为基础，针对不同分辨率做缩放设置, 实现Meta标签`viewport`的动态化:
```javascript
<script>
     if (/Android (\d+\.\d+)/.test(navigator.userAgent)) {
      if (parseFloat(RegExp.$1) > 2.3) {
       var phoneScale = parseInt(window.screen.width) / 640;
       document.write('<meta name="viewport" content="width=640, minimum-scale=' + phoneScale + ', maximum-scale=' + phoneScale + ', target-densitydpi=device-dpi" />');
      } else {
       document.write('<meta name="viewport" content="width=640, target-densitydpi=device-dpi" />');
      }
     } else {
      document.write('<meta name="viewport" content="width=640,user-scalable=no, target-densitydpi=device-dpi" />');
     }
 </script>
```

wap适配:

 前端中心暂时以淘宝的[lib-flexible](https://github.com/amfe/lib-flexible)为基础，结合自身的情况，整理了一套解决方案。先暂时试行，以后再慢慢完善。

**实现：**

**第一步 ： 新建html模板**

lib-flexible库的使用方法非常的简单，只需要在Web页面的
中添加对应的flexible_css.js,flexible.js文件，需要注意两个文件的书写顺序：
第一种方法是将文件下载到你的项目中，然后通过相对路径添加:
```
<script src="build/flexible_css.js"></script>
<script src="build/flexible.js"></script>
```

或者直接加载阿里CDN的文件：
```
<script src="http://g.tbcdn.cn/mtb/lib-flexible/0.3.4/??flexible_css.js,flexible.js"></script>
```

修改后的地址：[flexible.js](https://bradenhan.gitbooks.io/front-end/content/mobile/flexible.js)、[flexible_css.js](https://bradenhan.gitbooks.io/front-end/content/mobile/flexible_css.js)，我们需要用这个 。
　
HTML:

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta content="yes" name="apple-mobile-web-app-capable">
        <meta content="yes" name="apple-touch-fullscreen">
        <meta content="telephone=no,email=no" name="format-detection">
        <script src="build/flexible_css.js"></script>
        script src="build/flexible.js"></script>
        <link rel="apple-touch-icon" href="favicon.png">
        <link rel="Shortcut Icon" href="favicon.png" type="image/x-icon">
        <title>再来一波</title>
    </head>
    <body>
        <!-- 页面结构写在这里 -->
    </body>
</html>
```

**第二步： 把视觉稿中的px转换成rem**

目前Flexible会将视觉稿分成16份，而每一份被称为一个单位rem。针对我们这份视觉稿可以计算出：
1rem = 640/16=40px
`<html>`对应的font-size为40px：
这样一来，对于视觉稿上的元素尺寸换算，只需要原始的px值除以rem基准值即可。例如此例视觉稿中的图片，其尺寸是100px 100px,转换成为2.5rem 2.5rem。
快速计算方法 在实际生产当中，如果每一次计算px转换rem，会觉得非常麻烦，直接影响大家的开发效率。为了能让大家更快进行转换，前端这边找了一个小的工具，可以吧px转换rem，写的时候按照像素就好，会直接转换成相应尺寸的rem。
[cssrem](https://github.com/flashlizi/cssrem) 是一个CSS的px值转rem值的Sublime Text3自动完成插件。这个插件是由@正霖编写。配置: https://github.com/flashlizi/cssrem

**字号不使用rem**

前面我们见证了如何使用rem来完成H5适配。那么文本又将如何处理适配。是不是也通过rem来做自动适配。
显然，我们在iPhone3G和iPhone4的Retina屏下面，希望看到的文本字号是相同的。也就是说，我们不希望文本在Retina屏幕下变小，另外，我们希望在大屏手机上看到更多文本，以及，现在绝大多数的字体文件都自带一些点阵尺寸，通常是16px和24px，所以我们不希望出现13px和15px这样的奇葩尺寸。
如此一来，就决定了在制作H5的页面中，rem并不适合用到段落文本上。所以在Flexible整个适配方案中，考虑文本还是使用px作为单位。只不过使用[data-dpr]属性来区分不同dpr下的文本字号大小。
> .selector { width: 2rem; border: 1px solid #ddd; } [data-dpr="1"] .selector { height: 32px; font-size: 14px; } [data-dpr="2"] .selector { height: 64px; font-size: 28px; } [data-dpr="3"] .selector { height: 96px; font-size: 42px; }

其实H5适配的方案有很多种，网上有关于这方面的教程也非常的多。不管哪种方法，都有其自己的优势和劣势。而我们主要介绍的是如何使用Flexible这样的一库来完成H5页面的终端适配。为什么推荐使用Flexible库来做H5页面的终端设备适配呢？主要因为这个库在手淘已经使用了近一年，而且已达到了较为稳定的状态。除此之外，你不需要考虑如何对元素进行折算，可以根据对应的视觉稿，直接切入。

#### 参考资料
　
- [lib.flexible - 淘宝移动端自适应方案](https://github.com/amfe/lib-flexible)
- [使用Flexible实现手淘H5页面的终端适配](http://web.jobbole.com/84285/)
- [viewports剖析](http://www.w3cplus.com/css/viewports.html)
- [移动端高清、多屏适配方案](http://www.html-js.com/article/Mobile-terminal-H5-mobile-terminal-HD-multi-screen-adaptation-scheme%203041)
- [移动端屏幕适配viewport](http://www.ituring.com.cn/article/130015)
- [移动端适配基础(rem,vw,vh)](https://segmentfault.com/a/1190000003101394)
- [CSS值转REM的Sublime Text插件 - GitHub](https://github.com/flashlizi/cssrem)


## 代码存储
推荐Git, 不过由于公司内部使用的是SVN，所以给出的建议是:

Git进行本地版本控制管理，并写`.gitignore`来忽略掉一些生成文件，带完成一部分开发后，并入SVN管理。

## 兼容性和测试

测试原则

- 为 PC 构建的网页需在交付测试前自行进行 IE7/8/9/10、Firefox、Chrome 的测试；
- 尽量保证它们在各个浏览器表现一致，除非有特别的需求；
- 保证页面在没有 CSS 和脚本支持时的可用性；当没有脚本支持时，页面表现应当与有脚本支持但尚未操作时一致；
- 为移动设备构建的页面应根据产品需求方的要求考虑兼容性；

> 具体情况可询问 测试人员。

## 工具箱


[HTMLelement.info](http://htmlelement.info/)

[Can I use](http://caniuse.com/)

[垂直居中](http://howtocenterincss.com/)

[Mastering the :nth-child](http://nthmaster.com/)

[Regulex](https://jex.im/regulex)

[YOU MIGHT NOT NEED JQUERY](http://youmightnotneedjquery.com/)

[Flexbox in 5 minutes](http://flexboxin5.com/)

待续...

## 参考

[编码规范 by @mdo](http://codeguide.bootcss.com/)

[Baidu 前端规范](https://github.com/ecomfe/spec)

[Qunar 前端规范](https://github.com/doyoe/html-css-guide)

[常用的 HTML 头部标签](https://github.com/yisibl/blog/issues/1)

[Google Style Guide](http://docs.kissyui.com/1.4/docs/html/tutorials/style-guide/google-js-style.html)

[Amazeui Style Guide](http://amazeui.org/getting-started/)

[CSS Guidelines](http://cssguidelin.es/)

[20 Snippets You should be using from Html5 Boilerplate](http://www.1stwebdesigner.com/snippets-html5-boilerplate/)

[谈谈CSS性能](http://www.w3.org/2015/Talks/0109-CSSConf-xq/)

[Web动画性能指南](http://alexorz.github.io/animation-performance-guide/)

[Why Moving Elements With Translate() Is Better Than Pos:abs Top/left](http://www.paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/)

[High Performance Animations](http://www.html5rocks.com/zh/tutorials/speed/high-performance-animations/)

[jQuery Standards](http://lab.abhinayrathore.com/jquery-standards/)

[Learn jQuery](http://learn.jquery.com/about-jquery/)

[无线Web开发经验谈](http://am-team.github.io/amg/dev-exp-doc.html)

[移动端前端笔记大全](http://segmentfault.com/a/1190000002581619)