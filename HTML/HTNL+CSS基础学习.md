# html + css 基础
## 术语

术语就是行话，或者说是行业里的普通话，多掌握术语可以降低沟通成本

1. XML
   可扩展的标记语言：extension markup language，用于定义文档结构

```xml
<任务>
    <执行日期> 工作日 </执行日期>
    <执行时间> 上午十点 </执行时间>
    <执行内容> 写日志 </执行内容>
</任务>
```

2. HTML CSS
   HTML，CSS都是W3C组织定义的语言标准

   - HTML用于描述页面结构的语言，全称为Hyper Text Markup Language，超文本标记语言
   - CSS用于描述页面展示的语言，决定了页面长什么样子

3. XHTML
   可以认为是HTML的一种一个版本，要求更为严格，完全符合XML的规范（现在很少使用）

4. 浏览器（浏览器很重要，之后要专门花时间去研究浏览器）
   shekk：外壳
   core：内核（JS执行引擎、渲染引擎），执行html、css、js，渲染页面
   - IE：Trident内核
   - Firfox：Gecko内核
   - Chrome：Webkit（之前）/Blink（现在）内核
   - Safari：Webkit内核
   - Opera：Presto/Blink内核
   - 据说华为在研发浏览器内核，期待～
5. web
   互联网
6. w3c
   万维网联盟，非盈利性的组织：w3.org，为互联网提供各种标准

## 版本和兼容性

1. HTML5、CSS3

- HTML5：2014年制定完成
- CSS3：目前还没有制定完成

## 注释

为代码的阅读者提供帮助，不参与运行
在HTML中，注释使用如下格式书写：`<!-- 注释内容 -->`
大多数编辑器快捷键：ctrl/command + ？  alt/option + shift + a

## HTML基础
HTML（超文本标记语言——HyperText Markup Language）是构成 Web 世界的一砖一瓦。它定义了网页内容的含义和结构。除 HTML 以外的其它技术则通常用来描述一个网页的表现与展示效果（如 CSS），或功能与行为（如 JavaScript）。“超文本”（hypertext）是指连接单个网站内或多个网站间的网页的链接。链接是网络的一个基本方面。HTML 使用“标记”（markup）来注明文本、图片和其他内容，以便于在 Web 浏览器中显示。HTML 标记包含一些特殊“元素”如 `<head>、<title>、<body>、<header>、<footer>、<article>、<section>、<p>、<div>、<span>、<img>、<aside>、<audio>、<canvas>、<datalist>、<details>、<embed>、<nav>、<output>、<progress>、<video>、<ul>、<ol>、<li>` 等等。

HTML 元素通过“标签”（tag）将文本从文档中引出，标签由在“<”和“>”中包裹的元素名组成，HTML 标签里的元素名不区分大小写。也就是说，它们可以用大写，小写或混合形式书写。例如，`<title>` 标签可以写成 `<Title>`，`<TITLE>` 或以任何其他方式。然而，习惯上与实践上都推荐将标签名全部小写。
### 元素

其他叫法：标签、标记

- 整体：element（元素）
- 元素 = 起始标记（begin tag） + 元素内容 + 结束标记 （end tag）
- 属性 = 属性名 + 属性值
  `<a href = ""> </a>` a为元素，href为属性

### 属性的分类：

1. 局部属性：某些元素特有的属性，如 href
2. 全局属性：所有元素通用的属性，如 class
3. 空元素：没有**结束标记**的元素，两种写法，<...>和<.../>，如 `<meta charset="UTF-8"> <meta charset="UTF-8" />`

### 元素的嵌套

元素不能相互嵌套，元素的嵌套关系可以称为：父元素、子元素、祖先元素（越两级）、后代元素（越两级）、兄弟元素（拥有同一个父级元素）

### 标准结构文档

HTML：页面、HTML文档

- `<!DOCTYPE html>` 文档声明，告诉浏览器当前使用的HTML标准是HTML5不写文档声明将导致浏览器进入怪异渲染模式
- `<html lang="en"></html>` 根元素，一个页面最多只能有一个，并且该元素是所有其他元素的父元素或祖先元素，HTML5中不强制要求书写
  - lang属性：language，全局属性，表示该元素内部使用的文字是使用哪一种自然语言书写而成的
- `<head></head>` ：文档头，文档头部内容，不会显现在页面中
- `<meta>` ：文档的元数据，附加信息
  - charset属性：指定网页内容编码，值为字典
  - 字典，字符编码表，中国，GB2312；台湾，GBK ；一般使用 UTF-8，UTF-8 是 Unicode 编码的一个版本，非常常用，全球通用
  - `<meta name="viewport" content="width=device-width, initial-scale=1.0">`:适配移动端
- `<title>Document</title>`：网页标题
- `<body></body>`：文档体，网页内容页面上所有要参与显示的元素，都应该放置到文档体中

### 语义化

绝大部分HTML元素都有具体的含义，像a元素表示超链接，p元素表示段落，h1元素表示一级标题，但所有元素的含义都与展示效果无关，元素展示到页面中的效果，应该由CSS决定因为浏览器带有默认的CSS样式，所以每个元素有一些默认样式，这些默认样式都是可以修改的，所以开发过程中选择什么元素，取决于内容的含义，而不是显示出的效果
Web语义化是指使用具有语义的html标签、或语义化的class类名等内容，让页面具有清晰的结构与含义，从而让浏览器和开发者都能快速理解网页内容语义化的web页面一方面可以让机器更快的收集并研究网页的信息，读懂网页的内容，将收集汇总的信息进行分析，使结果能够被用户使用，也更便于屏幕阅读器（视障访客）读懂网页内容；另一方面它可以让开发人员更容易读懂网页结构，便于阅读维护

1. 每一个HTML元素都有具体的含义
   a元素：超链接
   cursor: pointer; 使鼠标变为小手
   p元素：段落
   h1元素：一级标题
2. 所有元素与显示效果是没有关系的，元素展示的页面效果是由css决定的，因为浏览器带有默认的css，所以每个元素带有一些默认的样式
   选择什么元素，取决于内容的含义，而不是显现出的效果

### 为什么需要语义化？

1. 为了搜索引擎优化（SEO）
   WEB 语义化可以让搜索引擎的爬虫更容易爬取到当前，从而提高网页的流量，即利用搜索引擎的规则提高网站在有关搜索引擎内的自然排名，语意化越好，搜索引擎越能理解网页每隔一段时间（一天或者几个小时），搜索引擎会从整个互联网中抓取页面源代码，然后为网页建立索引存储在数据库中，在响应用户的关键词搜索时，对数据库中的相关网页进行排序并返回搜索引擎：百度、搜搜、Bing、Google等
2. 为了让浏览器更好更快的理解网页，便于屏幕阅读器（视障访客）读懂网页内容
3. 便于开发者对代码进行阅读和维护

### 文本元素

HTML5中支持的元素：

#### h

标题：head，h1 ~ h6，一级标题到六级标题

#### p

段落，paragraph

> 在一些编辑器中可以使用 lorem 生成乱数假文，没有实际含义
> ((h&>{章节})+p>lorem)*6 快捷输入

#### span[无语义]

没有语义，仅用于设置样式

> 某些元素在显示时会独占一行（以前叫块级元素，到了HTML5已经弃用这种说法了），某些不会（以前叫行级元素，到了HTML5已经弃用这种说法了）

#### pre

预格式化文本元素
空白折叠：在源代码中的连续空白字符（空格、换行、制表），在页面显示时会被折叠为一个空格
例外：在pre元素中的内容不会出现空白折叠，在pre元素中出现的内容，会按照源代码格式显示到页面上
pre元素功能的本质是它有一个默认的css属性

> 显示代码时，通常外面套code元素，code表示代码区域

#### HTML实体（用的时候查字典）

实体字符，HTML Entity，通常用于在页面中显示一些特殊符号

1. & + 单词；
2. &# + 数字；

- 小于符号：&lt
- 大于符号：&gt
- 空格符号：&nbsp
- 版权符号：&copy
- &符号：&amp

#### a元素

超链接

### 元素属性
#### href属性

hyper reference（引用）：表示跳转地址

1. 跳转地址，普通链接
2. 锚链接，跳转到某个锚点
3. 功能连接
   点击后，触发某个功能

- 执行JS代码：javascript;
- 发送邮件：mailto:(要求用户计算机上安装有发送邮件的软件：exchange)
- 拨号：tel:（要求用户计算机上有拨号软件或在移动端访问）

#### id属性

全局属性，表示元素在文档中的唯一编号

#### target属性

表示跳转窗口位置
target的取值：

- _self：在当前窗口中打开
- _blank：在新窗口中打开

#### title属性

提示文字

### 路径的写法

#### 站内资源和站外资源

- 站内资源：当前网站的资源
- 站外资源：非当前网站的资源

#### 绝对路径和相对路径

站外资源：（只能使用）绝对路径
站内资源：使用相对路径（也可以使用绝对路径）

- 绝对路径的书写格式：
  - url地址：协议名://主机名:端口号/路径
    [https://weibo.com/](https://weibo.com/)
    [http://127.0.0.1:5500/index.html#](http://127.0.0.1:5500/index.html#)
  - 协议名：http、https、file（本地文件），当跳转目标和当前页面的协议相同时，可以省略协议
  - 主机名：域名、IP地址
  - 端口号：如果协议是http协议，默认端口号是80，如果协议是https，默认端口号是443
- 相对路径
  连接当前网站的资源
   - 以./开头，./表示当前资源所在的目录，相对路径中./可以省略
   - ../表示返回上一级

### 图片元素

#### img元素

image的缩写，空元素

- src属性：source，资源地址
- alt属性：当图片资源失效的时候，将使用该属性的文字代替图片

##### 和a元素联用

嵌套在a元素里

##### 和map元素联用

map的子元素：area，区域，地图，衡量坐标时，为了避免衡量误差，需要使用专业的衡量工具

```html
<area shape(形状)="circle（圆形）"coords(坐标)="399,223,48(半径)"href=""alt="">
<area shape(形状)="rect（矩形）"coords(坐标)="399,223,420,260(左上角和右下角坐标)"href=""alt="">
<area shape(形状)="poly（多边形）"coords(坐标)="399,223,420,260，630,657(顺时针依次描述每一个点的坐标)"href=""alt="">
<!--坐标系原点在左上角，向右x增加，向下y增加，找形状的形心-->
```

##### 和figure元素联用

指代、定义，通常用于把图片、图片标题、描述包裹起来，把图片和文字放在figure元素里，浏览器默认图片和文字相关

- 子元素：figcaption

```html
<a target="_blank" href="https://baike.baidu.com/item/%E5%A4%AA%E9%98%B3%E7%B3%BB/173281?fr=aladdin">
  <img usemap="#solarMap" src="./solar.jpg" alt="这是一张太阳系的图片">
</a>
<figcaption>
  <h2>太阳系</h2>
</figcaption>
<p>
  太阳系是以太阳为中心，和所有受到太阳的引力约束天体的集合体包括八大行星（由离太阳从近到远的顺序：水星、金星、地球、火星、木星、土星、天王星、海王星）、以及至少173颗已知的卫星、5颗已经辨认出来的矮行星和数以亿计的太阳系小天体,和哈雷彗星
</p>
```

### 多媒体元素（更多详见MDN）

#### video 视频

- controls：控制控件的显示,布尔属性，只能取值为controls，即：controls="controls"
  某些属性只有两种状态：1 不写；2 取值为属性名，这种属性叫做布尔属性
  布尔属性：在HTML5中可以不用书写属性值
   - 如果你没有指定 controls 属性，那么视频不会展示浏览器自带的控件，你也可以用 JavaScript 和 [HTMLMediaElement](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLMediaElement) API 来创建你自己的控件
- autoplay，自动播放，布尔属性
- muted：静音播放，布尔属性
- loop：循环播放，布尔属性

#### audio 音频

属性与video基本完全一样

```html
<video controls>
  <source src="myVideo.mp4" type="video/mp4">
  <source src="myVideo.webm" type="video/webm">
  <p>Your browser doesn't support HTML5 video. Here is
     a <a href="myVideo.mp4">link to the video</a> instead.</p>
</video>
```

#### 兼容性

1. 旧版本浏览器不支持这两个元素，只支持flash
2. 不同的浏览器支持的音视频格式不一致，视频一般有两种：mp4、webm，音频是mp3，通常一个网站做多个格式的视频，浏览器将会使用它所支持的第一个源          

### 列表元素

#### 有序列表

- ol：ordered list
- li：list item
  - type属性（能不用就不用）：
    - 取值1按1234排列
    - 取值一，按一二三四排列
    - 取值为I，按罗马数字排列
    - 取值为a或A，类推
  - reversed元素：
    - 倒序显示

#### 无序列表

无序列表常用于制作菜单 或 新闻列表

- ul：unordered list
- li
  - list-style: none;清除前边的标点

> 列表可以包含列表
> ul_5>(li>h3>a>lorem5)+(li_6>a>lorem5)

#### 定义列表

通常用于定义一些术语的定义

- dl：definition list 定义列表  列表
- dt：definition title 定义标题  标题
- dd：definition description 定义解释  内容

### 容器元素

该元素代表一个块元素，内部可以放置其他元素

#### div元素

没有语义

#### 语义化容器元素

- header：通常用于表示页头，也可以用于表示文章的头部
- footer：通常用于表示页角，也可以用于表示文章的尾部
- article：通常用于表示整篇文章
- section：通常用于表示文章的章节
- aside：通常用于表示侧边栏（一些附加信息）

```html
<header>页头</header>
<article>
  <header>文章标题</header>
  <section>文章章节内容</section>
</article>
<aside>侧边栏</aside>
<footer>页脚</footer>
```

#### nav元素

HTML5新元素，表示导航，只能用于菜单

### 元素的包含关系

可以在MDN对“[内容分类](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/Content_categories)”进行深入学习  

- 以前：块级元素可以包含行级元素，反过来不行（a元素除外)
- 现在：元素的包含关系由元素的内容类别决定，一切从语义化出发，更加复杂，元素包涵关系不清楚的去MDN上查阅

1. 容器元素中可以包含任何元素
2. a元素中几乎可以包含任何元素
3. 某些元素有固定的的子元素(ul>li,ol>li,dl>dd+dt)
4. 标题元素和段落元素不能相互嵌套，并且不能包含容器元素

## CSS基础
层叠样式表（Cascading Style Sheets，缩写为 CSS）是一种样式表语言，用来描述 HTML 或 XML（包括如 SVG、MathML 或 XHTML 之类的 XML 分支语言）文档的呈现。CSS 描述了在屏幕、纸质、音频等其它媒体上的元素应该如何被渲染的问题。CSS 是开放 Web 的核心语言之一，并根据 W3C 规范在 Web 浏览器中进行了标准化。以前，CSS 规范的各个部分的开发是同步进行的，这种方式允许对最新推荐的 CSS 版本进行控制。你可能已经听说过 CSS1、CSS2.1 甚至 CSS3。但是以后将不会再有 CSS3 或者 CSS4；相反，现在的一切都是没有版本号的 CSS。
在 CSS2.1 之后，规范的制定范围不断地增加，并且不同的 CSS 模块进展差异如此之大，以至于按照模块来单独进行开发并发布建议变得更加有效。W3C 现在不再对 CSS 规范进行版本控制，而是定期对 CSS 规范的最新稳定状态和各个模块的进展用快照来记录。CSS 模块现在有版本号或者级别，例如 CSS Color Module Level 5。
### 术语解释

CSS规则 = 选择器 + 声明块

 - 选择器：选中元素
 - 声明块:出现在大括号中{}，声明块中包含很多声明（属性），每一个声明（属性）表示某一个样式规则，用" ; "号结束

### calc运算方法

在css中可以对不同单位进行运算：calc();
calc(100% - 70px);

### css代码书写样式

1. 内部样式表，书写在style元素中
2. 元素样式表（js使用有点用）
   直接书写在元素的style属性中
   style = "";
3. 外部样式表（推荐使用）
   将样式书写到独立的css文件中，使用link元素链接，link元素为空元素
   - 可以解决多页面样式重复的问题
   - 有利于浏览器缓存，从而提高页面响应速度
   - 有利于代码分离（HTML和css），更容易阅读和维护

### 常见样式声明

1. weight 
   宽度
2. height 
   高度

3. color
   元素内部的文字颜色
   - **预设值**：定义好的单词
   - **三原色/色值**：光学三原色(红、绿、蓝)，每个颜色可以用0-255之间的数字来表达，三个颜色的数字组合起来叫色值
   - rgb表示法：rgb（2,113,33)
   - hex（16进制）表示法（常用）：#红绿蓝  #008c8c
     - 淘宝红：#ff4400/#f40（可简写）
     - 黑色：#000000
     - 白色：#ffffff
     - 红：#ff0000
     - 绿：#00ff00
     - 蓝：#0000ff
     - 紫：#ff00ff
     - 青：#00ffff
     - 黄：#ffff00
     - 灰色：#cccccc
     - 马尔斯绿：#008c8c
     - 海沫绿：#00b7c3
  
4. background-color
   元素背景颜色

5. font-size
   元素内部文字的尺寸大小，每个元素必须有字体大小，如果没有声明，则直接使用父元素的字体大小，如果没有父元素，则使用基准字号
   - **单位**：
     - px：像素，绝对单位，可以简单的理解为文字的高度占多少个像素
     - em：相对单位，相对于父元素的字体大小
   - user agent，UA， 用户代理（浏览器）

6. font-weight
   文字粗细程度，可以取值为数字，也可以取值为预设值bold（加粗）、normal（普通）
   - strom元素可用于加粗，strong表示重要的、不能忽略的内容，默认加粗

7. font-family
   文字类型，必须用户计算机中有这个字体才会有效
   使用多个字体以匹配不同环境：

   - font-family：consolas,微软雅黑,Arial,sans-serif（让电脑自行选择一个非衬线字体使用）

   - sans-serif：非衬线字体，常用于网页显示，衬线字体往往用于印刷，印刷出来好看，网页上不好看

8. font-style
   字体样式，通常用它设置字体倾斜
   `font-style：italic;`
   - i元素，默认样式是倾斜字体；实际使用中，通常用它表示一个图标（icon）
   - em元素，表示强调的内容
  
9. text-decoration
   文本修饰样式，加下划线、中间线等
   - a元素，自带下划线
   - del元素，中间加一条横杠，表示错误文字或被移除的信息等
   - s元素，中间加条线，代表过期
  
10. text-indent
   首行文本缩进，通常中文写2em

11. line-height
   行高，每行文本的高度，该值越大，每行文本的距离越大，设置行高为容器的高度，可以让单行文本垂直居中
   - 行高可以设置为纯数字，表示相对当前元素的字体大小 `line-height:1.5;`
  
12. letter-spacing
    文字间隙
  
13. text-align
    元素内部文字水平的排列方式：靠左，居中，靠右

### 透明度

每个颜色都具有透明通道，0~1

- rgba（红、绿、蓝、alpha），a即表示透明，0.5为半透明
- hex：#红绿蓝透，**透**：00~ff，即 #ffffff00
- opacity属性，它设置的是整个元素的透明，它的取值是0 ~ 1

### 选择器   
#### 简单的选择器

1. ID选择器（尽量不用）
   - ID = "name"   一对一，即元素的id不能重复，使用时前边加" # "号：#name
   - 因为其不可重复性，所以在没有必须使用id选择器的理由时便永远不要使用id选择器
  
2. 元素选择器
   
3. 类选择器（用的最多）
   class = "name"  一对多，即元素的class可以重复，使用时前边加" . "号 ：.name

4. 通配符选择器
   `*{}`表示所有元素被选中

5. 属性选择器
   根据属性名或属性值选择元素
   `[href]{}`表示选中所有href属性的元素
   `[href = "[http](http://www.baidu.com)"]{}`选中有href属性且属性值是`[http](http://www.baidu.com)`的元素
   `[class~=b]{}`选中有class属性且属性名为b的元素
   `[class*=b]{}`选中有class属性且属性中包含有b的元素

6. 伪类选择器（用的很多）
   选中某些元素的某种状态
   - link：超链接未访问时的状态`:link{ color:blue; }`
   - visited：超链接访问过后的状态`:visited{ color:yellow; }`
   - hover：鼠标移动上去(悬停)的状态`:hover{ color:red; }`
   - active：鼠标按下时的状态`:active{ color:green; }`

  顺序 link>visited>hover>active

   - nth-child(n)：选中第n个元素，可用5n等表示5的倍数`:nth-child(5n){}`
     - 关键词：even，等于偶数2n；odd，表示奇数，等于2n+1
   - nth-of-type(n)：选中子元素中第几个被指定的子元素
   - first-child ：选中第一个子元素 `:first-child{}`
   - firs-of-type：选中子元素中第一个被指定的子元素 `:firs-of-type{}`
   - last-of-type：选中子元素中最后一个被指定的子元素 `:last-of-type{}`
   - last-child：选中最后一个子元素 `:last-child{}`

7. 伪元素选择器
   通常生成并选中某个元素内部的第一个子元素或最后一个子元素
   - before `::before{ content(内容):""; }`生成并选中某个元素内部的第一个子元素
   - after `::after{ content:""; }`生成并选中某个元素内部的最后一个子元素

    ```css
    .header ul li:hover::after{
    content: "";
    position: absolute;
    width: 100%;
    height: 4px;
    left: 0;
    bottom: -4px;
    background-color: #fff;
    } // 生成一个空白条
    ```

   - first-letter `::first-letter{}`选中第一个字母
   - first-line `::first-line{}`选中元素中第一行文字
   - selection `::selection{}`选中被用户框选中的文字

#### 选择器的组合

1. 并且，加 .
   `div.text{}`

2. 后代选择器，父子元素之间加空格，不是父子元素也可选中，符合上下级关系即可
   `div.text ul li{}`

3. 子元素，父子元素之间加 >，必须是父子元素才行
`div>ul>li{}`

4. 相邻兄弟元素，两个兄弟元素之间加 +
`div+span{}`

5. 后面出现的所有兄弟元素，加 ~
   `.special~li{}`类名为special的元素和之后所有li兄弟元素

#### 选择器的并列

多个选择器，用逗号 , 分隔
语法糖：`div, .special~li, p{}` 多个元素用同样的样式

### 层叠

- 声明冲突：同一个样式，多次应用到同一个元素，很有用的一种修改全局样式下局部样式的方法
- 层叠：解决声明冲突的过程，浏览器自动处理（权重计算）

1. 比较重要性

  > 作者样式表：开发者书写的样式

  	重要性从高到低：

   - 作者样式表中的!important样式 `color:"red"!important;`
   - 作者样式表中的普通样式
   - 浏览器默认样式表中的样式

2. 比较特殊性
   主要看选择器
   - 总体规则：选择器选中的范围越窄，越特殊
   - 具体规则：通过选择器，计算出一个4位数（xxxx）
     - 千位：如果内联样式，记作1，否则记0,
     - 百位：等于选择器中所有ID选择器的数量
     - 十位：等于选择器中所有类选择器、属性选择器、伪类选择器的数量和
     - 个位：等于选择器中所有元素选择器和伪元素选择器的数量和

  **四位数不是逢十进一，而是逢256进1，分开比较四个数字，谁大谁显示**

3. 比较源次序
   代码书写靠后的胜出，css执行也是一行一行执行的，后边的覆盖前边的

#### 层叠的应用

1. 重置样式表
   书写一些作者样式，覆盖浏览器的默认样式，书写自己想要元素渲染出来的样式
   网上常见的重置样式表（别人初始化的，可以拿来即用）：normalize.css、reset.css、meyer.css
2. 爱恨法则
   link > visited > hover > active

### 继承

子元素会继承父元素的某些css属性，通常跟文字内容相关的属性都能被继承

- inherit  手动（强制）继承 `color:inherit;`
- initial：初始值，将该属性设置为默认值 ，即浏览器赋予的属性值 `color:initial;`

### 属性值的计算过程

渲染每个元素的前提条件是该元素的所有css属性必须有值，一个元素，从所有属性都没有值，到所有的属性都有值，这个计算过程，叫做属性值计算过程

1. 确定声明值：参考样式表中如果没有冲突的声明，则使用声明值作为css属性值
2. 层叠冲突：对样式表有冲突的声明使用层叠规则来确定css属性值
3. 使用继承：如果没有声明属性值，若可以继承，则继承父元素的值
4. 使用默认值：对仍然没有值的属性，使用浏览器默认值

![image.png](../.vuepress/public/images/note/html+css/1.png)

### 盒模型

- box：盒子，每个元素在页面中都会生成一个矩形区域（盒子）
- 盒子类型：
  - 行盒，display等于inline的元素，在页面中不换行
  - 块盒，display等于block的元素，在页面中独占一行
- display默认为inline
- 浏览器默认样式表设置的块盒：容器元素、h1~h6、p
- 浏览器默认样式表设置的行盒：span、a、img、video、audio

#### 盒子的组成部分

无论是行盒还是块盒，都有下边几个部分组成，从内到外分别是：

1. 内容 content
   - width、height，设置盒子内容的宽高
   - 内容部分通常叫做整个盒子的**内容盒 content-box**
2. 填充 padding
   - 盒子边框到盒子内容的距离
   - padding-left、padding-right、padding-top、padding-bottom
   - padding：上 右 下 左;（简写属性，中间空格，顺时针，同时设置4个）
   - 填充区 + 内容区 = **填充盒 padding-box**
3. 边框 border
   - 边框 = 边框样式（border-style） + 边框宽度（border-width） + 边框颜色（border-color）
   - border-style:solid;  实线边框
   - 边框样式：border-style
   - 边框宽度：border-width
   - 边框颜色：border-color
   - 边框区域 + 填充区 + 内容区 = **边框盒 border-box**
4. 外边距 margin
   - 边框到其他盒子之间的距离
   - margin-top、margin-left、margin-right、margin-bottom
   - margin: 上 右 下 左;（简写属性，中间空格，顺时针，同时设置4个）

#### 盒模型应用

##### 改变宽高范围

默认情况下，width和height设置的是内容盒宽高，衡量设计稿尺寸的时候，往往使用的是边框盒，但设置width和height设置的是内容盒，所以在设置宽高的时候容易出现尺寸误差，解决办法有：

1. 精确计算内容盒宽高和边框宽度
2. css3：box-sizing，改变width和height设置的盒子宽高为边框盒

##### 改变背景覆盖范围

默认情况下，背景覆盖边框盒，可以通过background-clip进行修改
`background-clip`设置元素的背景（背景图片或颜色）是否延伸到边框、内边距盒子、内容盒子下面
![image.png](../.vuepress/public/images/note/html+css/2.png)

##### 溢出处理

`over-flow`，控制内容溢出边框盒后的处理方式
![image.png](../.vuepress/public/images/note/html+css/3.png)

##### 断词规则

`word-break`，会影响文字在什么位置被截断换行
normal：普通、cjk字符（文字位置截断），非cjk字符（单词位置截断）
break-all：截断所有，所有字符都在文字处截断
keep-all：保持所有，所有文字都在单词之间截断，英文不变，中文一直不断
word-break：normal/break-all/keep-all

##### 空白处理

`white-space：nowrap；`不换行
`text-overflow：ellipsis；`单行文本文字溢出显示3个圆点，不溢出不出现，多行文本js处理

#### 行盒盒模型

常见的行盒：包含具体内容的元素`span、strong、em、i、img、video、audio`

##### 行盒模型显著特点

1. 盒子跟着内容延伸
2. 行盒不能设置宽高
   调整行盒的宽高应该使用字体大小、行高和字体类型，间接调整
3. 内边距（填充区）
   水平方向有效，垂直方向仅会影响背景，不会实际占据空间
4. 边框
   水平方向有效，垂直方向仅会影响背景，不会实际占据空间
5. 外边距
   水平方向有效，垂直方向不会实际占据空间

#### 行块盒

display:inline-block 的盒子

1. 不独占一行
2. 盒模型中所有尺寸都有效

##### 空白折叠

空白折叠发生在行盒（行块盒）内部或行盒（行块盒）之间，换行必然会产生空白折叠，除非一个挨一个写，或者用其他办法

### 可替换元素和非可替换元素

- 大部分元素，在页面上显示的结果，取决于元素的内容，称为**非可替换元素**
- 少部分元素，页面上显示的结果，取决于元素的属性，称为**可替换元素**
- 可替换元素：img、video、audio
- 绝大部分可替换元素都是行盒
- 可替换元素类似于行块盒，盒模型中所有尺寸都有效

### 常规流

- 盒模型：规定单个盒子的规则
- 视觉格式化模型：页面中的多个盒子排列规则
  - 视觉格式化模型，大体上将页面中盒子的排列分为三种方式：
    - 常规流
    - 浮动
    - 定位

#### 常规流布局

常规流布局又称常规流、文档流、普通文档流、常规文档流所有元素，默认情况下都属于常规流布局

- 总体规则：块盒独占一行，行盒水平依次排列
- 包含块（containing block）：每个盒子都有它的包含块，包含块决定了盒子的排列区域，绝大部分情况下：盒子的包含块为其父元素的内容盒
- **块盒**
  - 每个块盒的总宽度，必须刚好等于包含块的宽度
    - 宽度的默认值是auto，这里是将剩余空间吸收掉  auto：自动
    - margin的取值也可以是auto，不过是0
    - width吸收能力强于margin
    - 若宽度、边框、内边距和外边距计算后仍然有剩余空间，该剩余空间被margin-right全部吸收
    - 在常规流中，块盒在其包含块中居中，可以定宽，然后左右margin设置为auto
  - 每个块盒垂直方向上的auto值
    - height:auto,适应内容高度
    - margin:auto,表示0
  - 百分比取值
    - padding、宽高、margin可以取值为百分比，以上的所有百分比只相对于包含块的宽度，与高度没有任何关系，上下亦是相对于宽度
    - 最小宽度： min-width
    - 最大宽度： max-width
    - 高度的百分比：
      - 包含块的高度取决于子元素的高度，设置百分比无效
      - 包含块的高度不取决于子元素的高度，百分比相对于父元素高度
  - 上下外边距的合并
    - 两个常规流块盒，上下外边距相邻，会进行合并，且两个外边距取最大值
    - 不止兄弟元素，父子元素也合并，如果不想被合并，margin改成padding就行

### 浮动

#### 应用场景

- 文字环绕
- 横向排列

#### 浮动的基本特点

修改float属性值为：

- left：左浮动，元素靠上靠左排列
- right：右浮动，元素靠上靠右排列
- 默认值为none，不浮动
- 当一个元素浮动后，元素一定为块盒（更改display属性为block），行盒会改为块盒属性
- 浮动元素的包含块和常规流一样为父元素的内容盒

#### 盒子尺寸

- 宽度为auto时，适应内容宽度
- 高度为auto时，与常规流一致，适应内容的高度
- margin为auto时，为0
- 边框、内边距、百分比设置与常规流一样

#### 盒子排列

- 左浮动的盒子靠上靠左排列
- 右浮动的盒子考上靠右排列
- 浮动盒子在包含块中排列时，会避开常规流块盒
- 常规流盒子在包含块中排列时，无视浮动盒子
- 行盒在排列时，会避开浮动盒子
- 外边距合并不会发生，如果文字没有在行盒中，那么浏览器会直接生成一个行盒包裹文字，该行盒叫做匿名行盒

#### 高度坍塌

高度坍塌的根源：**常规流盒子的自动高度，在计算时不会考虑浮动盒子**
解决方式：

- 清除浮动，涉及css属性，clear
  - 默认值：none
  - left：清除左浮动，该元素必须出现在前面所有左浮动盒子的下方
  - right：清除右浮动，该元素必须出现在前面所有右浮动盒子的下方
  - both：清除左右浮动，该元素必须出现在前面所有左右浮动盒子的下方，即写一个空元素在浮动盒子下方加入清除浮动

```css
/* 伪元素解决(统一样式，直接可用),给浮动元素的父元素加上即可，伪元素默认为行级元素，clear只能清除块级元素浮动，所以需要把伪元素转为块级元素 */
::after{
content:"";
display:block;
clear:both;
}
```

### 定位

手动控制元素在包含块中的精准位置，涉及的css属性：position
一个元素，只要 position 的取值不是 static，认为该元素是一个定位元素，**定位元素会脱离文档流（相对定位除外）**

- 文档流中的元素摆放时，会忽略脱离了文档流的元素
- 文档流中元素计算自动高度时，会忽略脱离了文档流的元素

可以通过四个css属性设置其位置

- left
- right
- top
- bottom

#### position属性，绝对定位

- 默认值：static，静态定位（不定位）
- relative：相对定位
  - 主要用来提供包含块，不会导致元素脱离文档流，只是让元素在原来位置上可以进行偏移，盒子的偏移不会对其他盒子造成任何影响
- absolute：绝对定位
  - 宽高为auto，适应内容
  - 包含块变化：找祖先元素中第一个定位元素，该元素的填充盒为其包含块，若找不到，则为整个网页
- fixed：固定定位
  - 包含块不同：固定为视口（浏览器的可视窗口）
  - 其他情况与绝对定位完全一样

#### 定位下居中

某个方向居中：

- 定宽(高)
- 将左右（上下）距离设置为0
- 将左右（上下）margin设置为auto
- 绝对定位和固定定位中，margin为auto时，会自动吸收剩余空间

```css
{
position: fixed;
left: 0;
right: 0;
top: 0;
bottom: 0;
margin: auto;
}
```

#### 多个定位元素重叠时

- 称为堆叠上下文
- 设置z-index，通常情况下，该值越大越靠近用户，也就是说坐标z值越大
- 只有定位元素设置z-index有效
- z-index可以是负数，如果是负数，则遇到常规流、浮动元素，会被其覆盖

#### 特点

- 绝对定位、固定定位元素一定是块盒
- 绝对定位、固定定位元素一定不是浮动
- 没有外边距合并

### 其他样式

#### 透明度

- opacity，它设置的是整个元素的透明，它的取值是0 ~ 1
- 在颜色位置设置alpha通道(rgba )

#### 鼠标

使用css属性[cursor](https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor)设置

#### 盒子隐藏

- display:none，不生成盒子
- visibility:hidden，生成盒子，只是从视觉上移除盒子，盒子仍然占据空间

#### 背景图

背景图和img元素的区别:

  - img元素是属于HTML的概念
    - 当图片属于网页内容时，必须使用img元素
  - 背景图属于css的概念
    - 当图片仅用于美化页面时，必须使用背景图

##### 涉及的css属性

- [ background-image](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-image)
   - 设置背景图片的url
- [background-repeat](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-repeat)
  - 默认情况下，**背景图会在横坐标和纵坐标中进行重复**
- [background-size](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-size)
  - 预设值：contain、cover，类似于object-fit
  - 数值或百分比
  - `background-size: 100% 100%; `横向纵向撑满，也可以写数值，100px，200px；就是宽高
- [background-position](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-position)
  - 设置背景图的位置
  - 预设值：left、bottom、right、top、center（横向纵向居中），数值或百分比，数值表示左边和上方的距离
- background-attachment
  - 通常用它控制背景图是否固定，比如固定在视口`background-attachment:fixed;`
- background-color
  - 背景图和背景颜色混用，在相近颜色的地方加背景颜色
- background-clip
  - 设置背景图显示的区域，`background-clip: padding-box;`这里显示的是填充区
- 速写（简写）background
  - `background: url("") no-repeat 50% 50%（位置）/100% 100%（尺寸） fixed #ffffff;`
  - 顺序：图片地址 是否重复 位置/尺寸 是否固定 颜色
  - 位置和尺寸之间必须加一条斜杠，有些元素可以不写 

#### 雪碧图（精灵图 spirit）

一张图片里有很多小块，只用某些小块，这个大图片就叫雪碧图

## [HTML进阶](https://developer.mozilla.org/zh-CN/docs/Web/HTML)

### iframe元素

框架页（框架窗口），通常用于在网页中嵌入另一个页面窗口，也就是在一个网页有一个窗口可以打开显示另一个页面

- iframe 可替换元素
  - 可替换元素特点：
    - 通常是行盒
    - 通常显示的内容取决于元素的属性
    - CSS不能完全控制其中的样式，例如图片颜色等
    - 具有行快盒的特点
  - `target="myframe"` 设置这个属性即可在页面窗口打开其他网页

```html
<a href="https://www.baidu.com" target="myframe">百度</a>
<a href="https://douyu.com" target="myframe">斗鱼</a>
<a href="https://www.taobao.com" target="myframe">淘宝</a>
<iframe name="myframe" src="https://player.bilibili.com" scrolling="no" （不要滚动条）frameborder="no" （不要边框）framespacing="0"（框架间距为0） allowfullscreen="true"（允许全屏）>
```

### 表单元素

一系列元素，主要用于收集用户数据

#### input元素

输入框，文本输入

- type属性：表示输入框类型，常见取值
  - type: text，普通文本输入框
  - type: password，密码框
  - type: date, 日期选择框，兼容性问题
  - type: search, 搜索框，兼容性问题
  - type: number，数字输入框
  - type: checkbox，多选框
  - type: radio，单选框 
- value属性：表示输入框的值，就是文本框中的默认显示（提示）内容
- placeholder属性：显示提示的文本，文本框没有内容时显示，现在常用，点一下提示性文字还在，输入文字后消失
- input元素可以制作按钮，现在已经过时了，除非是兼容很古老的浏览器，否则不用
  - 当type值为reset、button、submit时，input表示按钮，可以通过value改按钮名字，最常用是button，自己定义功能

#### select元素

下拉列表选择框，通常和option元素配合使用

#### textarea元素

文本域，多行文本框

#### 按钮元素

button，type属性：reset、submit、button，分别是重置按钮、提交按钮、普通按钮，默认值submit

#### 表单状态

- readonly属性：布尔属性，是否只读，不会改变表单显示样式
- disabled属性：布尔属性，是否禁用，会改变表单显示样式

#### 配合表单元素的其他元素

##### label

普通元素，通常配合单选和多选框使用

-  显示关联
   设置id值，可以通过for属性，让label元素关联某一个表单元素，for属性书写表单元素id的值 
-  隐式关联 

##### datalist

数据列表，该元素本身不会显示到页面，通常用于和普通文本框配合

##### form元素

- 用来包含其他表单元素，通常，会将整个表单元素，放置form元素的内部，作用是当提交表单时，会将form元素内部的表单内容以合适的方式提交到服务器
- form元素对开发静态页面没有什么意义，目前了解一下，学了js和服务器就能用了
- action：提交地址

##### fieldset元素

- 表单分组，包裹住要分组列表
- 子元素legend表示标题

#### 美化表单元素

##### 新的伪类

###### focus

- :focus
  - 元素聚焦时的样式

###### checked

- :checked
  - 单选或多选框被选中的样式

```css
input:focus{
background-color: red;
color: royalblue;
}
input:checked{
  background-color: #fff;
  color: red;
}

```

##### 常见用法

- 重置表单元素样式

```css
input,textarea,button{
border: none;
}
input:focus,textarea:focus,button:focus{
outline: none;
outline-offset: none;
}
input[type="text"]{
border: 1px solid #999;
}
input[type="text"]:focus{
border: 1px solid skyblue;
}
```

- 设置textarea是否允许调整表单尺寸
  - css属性resize：
    - both：默认值，两个方向都可以调整尺寸
    - none：不能调整尺寸
    - horizontal: 水平方向可以调整尺寸
    - vertical：垂直方向可以调整尺寸
- 文本框边缘到内容的距离

```css
input,textarea
{
/ padding: 0 10px; /
text-indent: 1em;
}
```

- 控制单选和多选的样式

```css
.radio{
width: 12px;
height: 12px;
border: 1px solid #999;
border-radius: 50%;
cursor: pointer;
}
.radio.checked{
border-color: skyblue;
}
.radio.checked::after{
content: "";
display: block;
width: 5px;
height: 5px;
background-color: #008c8c;
margin-left: 3.5px;
margin-top: 3.5px;
border-radius: 50%;
}
```

### 表格元素

- 在css技术出现之前，网页通常使用表格布局，后台管理系统中也大多会使用表格
- 前台：面向用户
- 后台：面向管理员对界面要求不高，对功能性要求高
- 表格不再适用于网页布局主要是因为**表格的渲染速度过慢**
  - 标题caption
  - 表格table
  - 表头thead
  - 表体tbody
  - 表尾tfoot

```html
<table>
  <caption>这是表格标题</caption>
  <thead>
    <!-- table row -->
    <tr>
      <th>列1</th>
      <th>列2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>数据1</td>
      <td>数据2</td>
    </tr>
    <tr>
      <td>数据1</td>
      <td>数据2</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="2">合计：XXXX</td>
    </tr>
  </tfoot>
</table>
```

### 伪元素

伪元素天生就存在，存在于元素内，且是行级元素，如果要改变宽高需要改成块级元素，最常见的就是before和after，需要用css选中

- ::before  逻辑上最前边的伪元素，在元素之前，如：span::before{},代表在span之前
- ::after  逻辑上最后边的伪元素，在元素之后
  - content: 伪元素中的内容

### 其他元素

- meta
  写给浏览器读的东西，可以用于搜索引擎优化（SEO），给浏览器写一下提示性的关键字 
- link
  链接外部资源（CSS、图标）
   - rel属性：relation，链接的资源和当前网页的关系，如css是样式表stylesheet，图标是icon
   - type属性：链接的资源的MIME类型 
- abbr
  缩写词 
- time
  提供给浏览器或搜索引擎阅读的时间
  2019-5-20;datetime是给浏览器看的 
- b  （bold）
  以前是一个无语义元素，主要用于加粗字体 
- q
  表示引用一小段文本 
- blockquote
  表示大段引用的文本 
- br
  无语义,换行符，主要用于在文本中换行 
- hr
  无语义，主要用于分割，上下文加一条分割线

## [CSS进阶](https://developer.mozilla.org/zh-CN/docs/Web/CSS)

### at规则（@规则）

at-rule: @规则、@语句、CSS语句、CSS指令

- import
  - `@import "路径";`在css文件中先导入另外一个css文件，不用在html页面链接重置css文件，必须写到第一行
- charset
  - `@charset  "utf-8"; `在css中告诉浏览器该CSS文件使用的字符编码集是utf-8，必须写到css文件中的第一行

### web字体和图标

#### web字体

解决用户电脑上没有安装相应字体的问题，强制让用户下载该字体（强制帮用户临时下载安装，用户感知不到，后台下载，用户关闭浏览器后会自动消失）

- 使用@font-face指令制作一个新字体

```css
@font-face {font-family: "iconfont";
  src: url(''); /* IE9 */
  src: url('') format('embedded-opentype'), /* IE6-IE8 */
  url('data:application/x-font-woff2;charset=utf-8;base64,d09GMgABAAAAAARAAAsAAAAACIAAAAPxAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHEIGVgCDHAqEOIQCATYCJAMQCwoABCAFhG0HTBt4B8gOJQkJCp3LBgFAPEDr/v/M7jztvV9gkhucCOWfAEc2qTpB7f1YZ//SdAFndz84Xdw+gJWLDFrPpDxlPk4yj+QJ8LU+z+W45QHOb1kucwyKjnrRcRxQQGNsLZBAB0iCnkXsutnqwQSeJiBT1yCo34BpDRAvEicFhNkzJDPEeyxiQn1QLCiMWBmF/RCjONlhuIV9xvfDdx1DPImClHjWkKnjbTDqk/Blc8qjXEfKgVfnwm0dKVoDkTA90jMRtjKtYdmn1KgrUCy9k/BJ+LTg47zSKMmGoimmvzxSiUAoJNbmQWfKpnwSFImj9YFPwpd5sgXQRM1dzIfk4px51Sa+dIFUUlitrClfkE/J56eNGtjY3B8NOHOl7MmrUY8ejdh0rH+/VxtGv14w8iUftQHt3q8f6KuHXfv43paj+poFOY1SIsrtulRgWHuxV+ruy4V4w5WkJNnhlWAYHbfDKp7dsDK7YP2RpJQyG9CCNQh7qm2zc7SnT0eX7Xr8eKTWZ9vj/mlXXzd69WpqqNRf/eTJjNTTD+o+vBvvrcomKbLL2J6VqxHesCbHvIpHM44efbY8KPV8Bh+ljRgNGtc9CTGhJlSL043Sx+G998vM0cP3i6zGRy1A+WW9gun6sWtcU7IuVGpyu+rq2gY4imozPbH22Ktjwj21Zg1w8PMJpocPR2ZeqND05k3D3nUJFxIWTQYw8krP7MbGCpi1e3rNbh0aE8f+pQ5VmQhCBDWO0yN6Lqxz9WncU1Zf92vADzjLjIvcxZfLo9bloVYog0BCrU7PD5EB926XiT3y6e5egyQkodUz5TyQQ9lu47OP6XESkkhVYrjicaPTq+Oewd/qT8U/LrpWb84bkwTzAUofp2dwLk/hFJ77jw/hxIvgN54l/B8yLm3Yn/hcBG+Tu5VFuJRHyC49ktKP9JBLMzbFr1y0xvhWKJJfdTRVDFuwXibDgS5Q0fMqfFWA4wqK71IgUaQOUsUaUyKjNQrkdEahYj2RaWXi+pxKVFiIJWhpPkNQ3hEkynqAVHm3KZHxDAWq+oZC5QNGZlTI2jGnaVCysQupmVEbsYSJYvW4RdnOEs36Oir5nWbVLTdYTVTVlDipbtven59I3VStYo4WkGoYE4moelxkAjuPOp0e4lU9dmplgsyYd4ip3dSoJwlWjwsS9aWizBjKhrAIIxRWHm6i1p5JDHy+DiXxczJTEwg/gk0olUbpnqgmqMpAmahxZyLsSn9NgKQGw4jcOJHKw4WYABfllDIehDd6mB1lxQjkAimvIUzUSsyqEZrXudZwB2TER8aQhDTEUCBOnsH8seF5bkn2Z9rMbo1qshJS3MxvUcyewQAAAAA=') format('woff2'),
  url('../font/iconfont.woff?t=1558584078834') format('woff'),
  url('../font/iconfont.ttf?t=1558584078834') format('truetype'), /* chrome, firefox, opera, Safari, Android, iOS 4.2+ */
  url('../font/iconfont.svg?t=1558584078834#iconfont') format('svg'); /* iOS 4.1- */
}

.iconfont {
  font-family: "iconfont" !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.icon-ditu:before {
  content: "\e884";
  /* &#xe884; */
}

.icon-yonghu:before {
  content: "\e671";
}

.icon-danseshixintubiao-:before {
  content: "\e62e";
}
```

#### 字体图标

[iconfont.cn](https://www.iconfont.cn/)  阿里巴巴的字体图标库，也是字体，可以设置颜色、宽高等等，行盒，文字的特点

### 块格式化上下文

#### [BFC  block formatting context](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)

是Web页面的可视CSS渲染的一部分，是块盒子的布局过程发生的区域，也是浮动元素与其他元素交互的区域它是一个独立的渲染区域，它规定了在该区域中，常规流块盒的布局：

- 常规流块盒在水平方向上，必须撑满包含块
- 常规流块盒在包含块的垂直方向上依次摆放
- 常规流块盒若外边距无缝相邻，则进行外边距合并
- 常规流块盒的自动高度和摆放位置，无视浮动元素

块格式化上下文对浮动定位与清除浮动都很重要浮动定位和清除浮动时只会应用于同一个BFC内的元素浮动不会影响其它BFC中元素的布局，而清除浮动只能清除同一BFC中在它前面的元素的浮动外边距折叠也只会发生在属于同一BFC的块级元素之间

#### BFC渲染区域

这个区域由某个HTML元素创建，以下元素会在其内部创建bfc区域：

- 根元素（html）**意味着HTML元素创建的bfc区域覆盖了整个页面中所有的元素**
- 浮动元素（元素的 [float](https://developer.mozilla.org/zh-CN/docs/Web/CSS/float) 不是 none）
- 绝对定位元素（元素的 [position](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position) 为 absolute 或 fixed）
- 行内块元素（元素的 [display](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 为 inline-block）
- 表格单元格（元素的 [display](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 为 table-cell，HTML表格单元格默认为该值）
- 表格标题（元素的 [display](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 为 table-caption，HTML表格标题默认为该值）
- 匿名表格单元格元素（元素的 [display](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 为 table、table-row、 table-row-group、table-header-group、table-footer-group（分别是HTML table、row、tbody、thead、tfoot 的默认属性）或 inline-table）
- [overflow](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow) 计算值(Computed)不为 visible 的块元素
- [display](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 值为 [flow-root](https://drafts.csswg.org/css-display/#valdef-display-flow-root) 的元素
- [contain](https://developer.mozilla.org/zh-CN/docs/Web/CSS/contain) 值为 layout、content 或 paint 的元素
- 弹性元素（[display](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 为 flex 或 inline-flex 元素的直接子元素）
- 网格元素（[display](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 为 grid 或 inline-grid 元素的直接子元素）
- 多列容器（元素的 [column-count](https://developer.mozilla.org/zh-CN/docs/Web/CSS/column-count) 或 [column-width(en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/column-width) 不为 auto，包括 column-count 为 1）
- column-span 为 all 的元素始终会创建一个新的BFC，即使该元素没有包裹在一个多列容器中（[标准变更](https://github.com/w3c/csswg-drafts/commit/a8634b96900279916bd6c505fda88dda71d8ec51)，[Chrome bug](https://bugs.chromium.org/p/chromium/issues/detail?id=709362)）


不同的bfc区域，它们进行渲染时互不干扰，创建bfc的元素，隔绝了内部和外部的联系，内部的渲染不会影响到外部
具体规则：

- 创建bfc的元素，它的自动高度需要计算浮动元素，这里解决高度坍塌也可以用创建bfc的方法
- 创建bfc的元素，它的边框盒不会与浮动元素重叠
- 创建bfc的元素，不会和它的子元素进行外边距合并

### 布局

排列页面中的区域，大区域布局

#### 多栏布局

两栏布局、三栏布局等

#### 等高

- CSS3的弹性盒
- JS控制
- 伪等高

### 浮动的排列方式

- 左浮动向上向左排列
- 右浮动向上向右浮动
- 浮动盒子的顶边不得高于上一个盒子的顶边，一个挨一个，顺序依次排列
- 若剩余空间无法放下浮动的盒子，则该盒子向下移动，直到具备足够的空间能容纳盒子，然后再向左或向右排列

### 行高的取值

line-height，一般设置为纯数字，如1.5、2

- px, 像素值，固定字体大小，多行文本字体过大容易出现文字叠加
- 无单位的数字，先继承再计算，也就是先继承行高，再根据当前元素计算，line-height：2；   font-size：40px； 此时行高为80px
- em单位，字体大小的倍数，换算为px，先计算像素值，再继承，line-height：2em；   font-size：40px；此时行高为32px（浏览器默认16px时）
- 百分比，与em效果基本一样

### 画布 canvas

指一块区域
特点：

- 最小宽度为视口宽度
- 最小高度为视口高度

### svg

svg: scalable vector graphics，可缩放的矢量图

1. 该图片使用代码书写而成
2. 缩放不会失真
3. 内容轻量

svg可以嵌入浏览器，也可以单独成为一个文件
svg使用xml语言定义

### html元素的背景

覆盖画布，如果给html元素设置背景，相当于给画布设置背景

### body元素的背景

- 如果 HTML 元素有背景，body 元素背景正常（背景覆盖边框盒）
- 如果 HTML 元素没有背景，则 body 元素的背景覆盖画布（不正常）

### 关于画布背景图

背景图的位置和背景一样，两个都有 body 正常，HTML 没有 body 不正常

- 背景图的宽度百分比，相对于视口，背景颜色没问题，只有背景图只相当于视口
- 背景图的高度百分比，相对于网页高度（html元素高度），不是画布（body）也不是视口
- 背景图的横向位置百分比、预设值，都相对于视口
- 背景图的纵向位置百分比、预设值，都相对于网页高度
- 高度相对于html元素，宽度相对于视口

### 行盒的垂直对齐

#### 多个行盒垂直方向上的对齐

- 给没有对齐元素设置一个css属性：vertical-align，设置在行盒身上
- 预设值：middle（中线）、top、button、text-top...
- 数值：从0开始依次增加或减少调整就行

### 图片的底部白边

图片的父元素是一个块盒，块盒高度自动，图片底部和父元素底边之间往往会出现一条空白边，不加边框不容易看出来，但问题依然存在，解决办法：

- 设置父元素的字体大小为0，但会带来一些副作用，如果有文字就会看不见
- 将图片设置为块盒

### 参考线-深入理解字体

font-size、line-height、vertical-align、font-family

#### 文字

- 文字是通过一些文字制作软件制作的，比如fontforge
- 制作文字时，会有几根参考线，不同的文字类型，参考线不一样同一种文字类型，参考线一致

#### font-size

- 字体大小，设置的是文字的相对大小
- 文字的相对大小：1000、2048、1024
- 文字顶线到底线的距离，是文字的实际大小（content-area，内容区）
- 行盒的背景，覆盖content-area

#### 行高

- 顶线向上延伸的空间，和底线向下延伸的空间，两个空间相等，该空间叫做gap（空隙）
- gap默认情况下，是字体设计者决定
- top到botoom，即内容区加上空隙（看ppt图），叫做virtual-area（虚拟区）
- 行高，就是virtual-area
- line-height:normal，默认值，使用文字默认的gap
- 文字一定出现一行的最中间——错误，content-area一定出现在virtual-area的中间

#### vertical-align

- 决定参考线：font-size、font-family、line-height
- 一个元素如果子元素出现行盒，该元素内部也会产生参考线
- baseline：该元素的基线与父元素的基线对齐
- super: 该元素的基线与父元素的上基线对齐
- sub：该元素的基线与父元素的下基线对齐
- text-top: 该元素的virtual-area的顶边，对齐父元素的text-top
- text-bottom: 该元素的virtual-area的底边，对齐父元素的text-bottom
- top：该元素的virtual-area的定边，对齐line-box的顶边
- bottom：该元素的virtual-area的底边，对齐line-box的底边
- middle: 该元素的中线（content-area的一半），与父元素的X字母高度一半的位置对齐
- 行盒组合起来，可以形成多行，每一行的区域叫做line-box，line-box的顶边是该行内所有行盒最高顶边
- 底边是该行行盒的最低底边
- 实际，一个元素的实际占用高度（高度自动），高度的计算通过line-box计算
  - 行盒：inline-box
  - 行框：line-box
  - 数值：相对于基线的偏移量，向上为正数，向下为负数
  - 百分比：相对于基线的偏移量，百分比是相对于自身virtual-area的高度
- line-box是承载文字内容的必要条件，以下情况不生成行框：
  - 某元素内部没有任何行盒
  - 某元素字体大小为0

#### 可替换元素和行块盒的基线

- 图片：基线位置位于图片的下外边距
- 表单元素：基线位置在内容底边
- 行块盒：
  - 行块盒最后一行有line-box，用最后一行的基线作为整个行块盒的基线
  - 如果行块盒内部没有行盒，则使用下外边距作为基线

### 层叠上下文

[层叠上下文](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)（stack context），它是一块区域，这块区域由某个元素创建，它规定了该区域中的内容在Z轴上排列的先后顺序

#### 创建层叠上下文的元素

- 文档根元素（html）；
- [position](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position) 值为 absolute（绝对定位）或  relative（相对定位）且 [z-index](https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index) 值不为 auto 的元素；
- [position](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position) 值为 fixed（固定定位）或 sticky（粘滞定位）的元素（沾滞定位适配所有移动设备上的浏览器，但老的桌面浏览器不支持）；
- flex ([flexbox(en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)) 容器的子元素，且 [z-index](https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index) 值不为 auto；
- grid ([grid](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid)) 容器的子元素，且 [z-index](https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index) 值不为 auto；
- [opacity](https://developer.mozilla.org/zh-CN/docs/Web/CSS/opacity) 属性值小于 1 的元素（参见 [the specification for opacity](https://www.w3.org/TR/css3-color/#transparency)）；
- [mix-blend-mode](https://developer.mozilla.org/zh-CN/docs/Web/CSS/mix-blend-mode) 属性值不为 normal 的元素；
- 以下任意属性值不为 none 的元素：
  - [transform](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform)
  - [filter](https://developer.mozilla.org/zh-CN/docs/Web/CSS/filter)
  - [perspective](https://developer.mozilla.org/zh-CN/docs/Web/CSS/perspective)
  - [clip-path](https://developer.mozilla.org/zh-CN/docs/Web/CSS/clip-path)
  - [mask](https://developer.mozilla.org/zh-CN/docs/Web/CSS/mask) / [mask-image](https://developer.mozilla.org/zh-CN/docs/Web/CSS/mask-image) / [mask-border](https://developer.mozilla.org/zh-CN/docs/Web/CSS/mask-border)
- [isolation](https://developer.mozilla.org/zh-CN/docs/Web/CSS/isolation) 属性值为 isolate 的元素；
- [-webkit-overflow-scrolling](https://developer.mozilla.org/zh-CN/docs/Web/CSS/-webkit-overflow-scrolling) 属性值为 touch 的元素；
- [will-change](https://developer.mozilla.org/zh-CN/docs/Web/CSS/will-change) 值设定了任一属性而该属性在 non-initial 值时会创建层叠上下文的元素（参考[这篇文章](https://dev.opera.com/articles/css-will-change-property/)）；
- [contain](https://developer.mozilla.org/zh-CN/docs/Web/CSS/contain) 属性值为 layout、paint 或包含它们其中之一的合成值（比如 contain: strict、contain: content）的元素

在层叠上下文中，子元素同样也按照上面解释的规则进行层叠 重要的是，其子级层叠上下文的 z-index 值只在父级中才有意义子级层叠上下文被自动视为父级层叠上下文的一个独立单元

#### 同一个层叠上下文中元素在Z轴上的排列

从后到前的排列顺序：

1. 创建层叠上下文的元素的背景和边框
2. 层叠级别(z-index, stack level)为负值的层叠上下文，相同情况后边的覆盖前边的
3. 常规流非定位的块盒
4. 非定位的浮动盒子
5. 常规流非定位行盒
6. 任何 z-index 是 auto 的定位子元素，以及 z-index 是 0 的堆叠上下文
7. 层叠级别为正值的层叠上下文

#### 特点

- 层叠上下文可以包含在其他层叠上下文中，并且一起创建一个层叠上下文的层级
- 每个层叠上下文都完全独立于它的兄弟元素：当处理层叠时只考虑子元素
- 每个层叠上下文都是自包含的：当一个元素的内容发生层叠后，该元素将被作为整体在父级层叠上下文中按顺序进行层叠
- 层叠上下文的层级是 HTML 元素层级的一个子级，因为只有某些元素才会创建层叠上下文可以这样说，没有创建自己的层叠上下文的元素会被父层叠上下文同化

### 数据链接

data url
数据链接：将目标文件的数据直接书写到路径位置
语法：data: MIME, 数据

#### 意义

- 优点：
  - 减少了浏览器中的请求，减少了请求中浪费的时间
  - 有利于动态生成数据
- 缺点：
  - 增加了资源的体积，导致了传输内容增加，从而增加了单个资源的传输时间
  - 不利于浏览器的缓存，浏览器通常会缓存图片文件、css文件、js文件
  - 会增加原资源的体积到原来的4/3
- 应用场景：
  - 但请求单个图片体积较小，并且该图片因为各种原因，不适合制作雪碧图，可以使用数据链接
  - 图片由其他代码动态生成，并且图片较小，可以使用数据链接

### base64

一种编码方式，通常用于将一些二进制数据，用一个可书写的字符串表示

### 浏览器兼容性

#### 问题产生原因

- 市场竞争，标准没有发布
- 标准仍在讨论中（草案），浏览器厂商希望先支持

#### 厂商前缀

- IE： -ms-
- Chrome，safari:  -webkit-
- opera： -o-
- firefox: -moz-

浏览器在处理样式或元素时，使用如下的方式：当遇到无法识别的代码时，直接略过

#### 渐近增强和优雅降级

两种解决兼容性问题的思路，会影响代码的书写风格

- 渐近增强：先适应大部分浏览器，然后针对新版本浏览器加入新的样式
  - 书写代码时，先尽量避免书写有兼容性问题的代码，完成之后，再逐步加入新标准中的代码
- 优雅降级：先制作完整的功能，然后针对低版本浏览器进行特殊处理
  - 书写代码时，先不用特别在意兼容性，完成整个功能之后，再针对低版本浏览器处理样式

查找css兼容性的网站：[caniuse.com](https://caniuse.com/)

### 居中总结

居中：盒子在其包含块中居中

#### 行盒（行块盒）水平居中

直接设置行盒（行块盒）父元素`text-align:center`

#### 常规流块盒水平居中

先定宽，然后设置左右margin为auto

#### 绝对定位元素的水平居中

先定宽，然后设置左右的坐标为0（left:0, right:0），将左右margin设置为auto
实际上，固定定位（fixed）是绝对定位（absolute）的特殊情况，固定定位的居中方法是一样的

#### 单行文本的垂直居中

设置文本所在元素的行高line-height为整个区域的高度

#### 行块盒或块盒内多行文本的垂直居中

没有完美方案
设置盒子上下内边距padding相同，达到类似的效果

#### 绝对定位的垂直居中

定高，设置上下的坐标为0（top:0, bottom:0），将上下margin设置为auto

### 样式补充

#### display:list-item;

设置为该属性值的盒子，本质上仍然是一个块盒，但同时该盒子会附带另一个盒子，元素本身生成的盒子叫做主盒子，附带的盒子称为次盒子，次盒子和主盒子水平排列，而且排列顺序是先排列次盒子再排列主盒子
涉及的css：

1. `list-style-type`
   设置次盒子中内容的类型
2. `list-style-position`
   设置次盒子相对于主盒子的位置
3. 速写属性`list-style`
   先写类型再写位置
4. **清空次盒子**
   list-style: none

#### 图片失效时的宽高问题

如果img元素的图片链接无效，img元素的特性和普通行盒一样，无法设置宽高
可以设置为块盒或行块盒改为可以设置宽高

#### 行盒中包含行块盒或可替换元素

行盒的高度与它内部的行块盒或可替换元素的高度无关，里边是块盒的话高度会被撑开

#### text-align:

- left: 左对齐
- right：右对齐
- center：居中
- justify：除最后一行外，分散对齐，适应宽度，两端对齐

#### 制作一个三角形

```css
div{
width: 0;
height: 0;
border-width: 10px;
border-style: solid;
border-color: skyblue transparent transparent transparent;
}
```

#### direction 和 writing-mode

- 开始 start -> 结束 end
- 左 left -> 右 end
- 开始和结束是相对的，不同国家有不同的习惯
- 左右是绝对的
- direction设置的是开始到结束的方向, 
  - direction: ltr:从左到右
  - direction: rtl：从右到左
- writing-mode：设置文字书写方向
  - writing-mode：vertical-rl；从上到下从右到左