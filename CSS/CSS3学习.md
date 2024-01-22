# [CSS3](https://developer.mozilla.org/zh-CN/docs/Web/CSS)

CSS 是开放 Web 的核心语言之一，并根据 W3C 规范在 Web 浏览器中进行了标准化。以前，CSS 规范的各个部分的开发是同步进行的，这种方式允许对最新推荐的 CSS 版本进行控制。你可能已经听说过 CSS1、CSS2.1 甚至 CSS3。但是以后将不会再有 CSS3 或者 CSS4；相反，现在的一切都是没有版本号的 CSS。

## 加前缀只支持对应内核浏览器

加前缀是因为该属性最早(甚至现在任然)只由该家浏览器支持，为了兼容老版本浏览器
    
   - goole/safari  -webkit-
    
   - ie -ms-

   - firefox -o-
   
   - opera -moz-

### css手册
1. reference(参考) manual(手册) website(网站): http://css.doyoe.com

2. Authoritative(权威的) inquiry(查找) website: http://www.caniuse.com

## 插件

- 预处理器 pro-processor:
    less/sass(插件)  cssNext(插件)
    简化代码，先按照别人的格式写，再生成css代码，预处理，相当于设定预设对象，从对象里取要用的东西，对象里的东西改则代码跟着改
    cssNext 用来实现一些未来的标准的（未完全在各大浏览器兼容）

- 后处理器 post-processor：
    autoprefixer (插件)
    补齐缺少的带有前缀的属性，还是自己的代码格式，写完后帮咱们补充，后处理

- postCss(工具) + 插件 （充分体现扩展性，200多个）
    postCss是用js实现的css的抽象的语法树，很多插件基于语法树来进行接下来的编写
    AST(Abstract Syntax Tree)
    剩下的事留给后人来做

## css3选择器

### Relationship Selectors  选择器的关系模式

-  E+F 选中下一个满足条件的兄弟元素节点，也就是选中下一个满足条件的元素，只选中一个 
-  E~F 选中下面满足条件的所有兄弟元素节点，也就是选中接下来所有满足条件的元素 
-  E F 父子选择器 

### Attribute Selectors  属性选择器

-  E[attr~="val"] 属性值有独立的val才满足，也就是可以有其他值，但需用空格隔开 
-  E[attr|="val"] 属性值是val开头或val-开头的才满足 
-  E[attr^="val"] 属性值以val为开头的满足 
-  E[attr$="val"] 属性值以val为结尾的满足 
-  E[attr*="val"] 属性值里只要存在val就满足，不管在哪，val是空格也行 

### Pseudo-Element Selectors  伪元素选择器

-  E::placeholder 必须写两个冒号，只能改变H5里placeholder属性的字体颜色，兼容性差，几乎不用 
-  E::selection 必须写两个冒号，改变鼠标选中的字体的样式，只能设置三个属性，color、background-color、text-shadow(文字阴影，横偏值 纵偏值 颜色) 

### Pseudo-Classes Selectors  伪类选择器   被选中的元素的一种状态

-  E:not(selector) 选中除了selector的其他所有的 
-  E:root 根标签选择器，类似于HTML，改变全局，不只是HTML，也有可能是其他环境，可以直接写，即:root{},其前不用加选择器 
-  E:target 锚点，E是要改变的元素，E的id被href选中后，即可被跳转或改变，类似于location.hash = id 
-  E:first-child 选中只有E元素的队列里的第一个E元素，如li*6中的第一个li 
-  E:last-child 选中只有E元素的队列里的最后一个E元素，如li*6中的最后一个li 
-  E:only-child E是独生子的时候满足，队列里只有一个E元素，如里的span元素 
-  E:nth-child(n) n是从0开始查的，2n表示偶数，2n+1表示奇数，css从1开始查，也可填单词和数字，odd表示奇数，even表示偶数，考虑其他元素的影响，若n表示其他元素的占 位，则不会被选中 
-  E:nth-last-child(n) 倒着查，n还是一样 
-  E:first-of-type 选中第一个这个类型的，不考虑其他元素的影响，可共队列 
-  E:last-of-type 选中最后一个这个类型的 
-  E:only-of-type 队列中这个类型的元素只有一个的时候选中 
-  E:nth-of-type(n) 正着查，也是不考虑其他元素的影响，队列中这个类型的元素，若n表示其他元素的占位，则不会被选中 
-  E:nth-of-last-type(n) 反着查 
-  E:empty 元素内部为空的选中，没有任何节点，空格都不行，但注释行，注释不算做内容 
-  E:checked 改变[ ] 选中后的变化，可以通过::after做更改其他元素的简单操作,如span::after 
-  E:enabled 选中input搜索框能用的 
-  E:disabled 选中input搜索框不能用的 
-  E:read-only 选中input中有readonly属性的 
-  E:read-write 选中input中有readwrite属性的 

**calc(50% - 100px);**css中唯一能够使用计算的属性
**border-color的默认值为currentColor中转颜色,而currentColor取color的值**

## 属性

### border

-  border-radius: 左上 右上 右下 左下 
-  border-top-left-radius: 10px; 被正圆切割
   先写上下，再写左右 
-  border-top-left-radius: 10px 20px; 被椭圆切割，改变单边切割弧度 
-  border-top-left-radius: 10px 20px 30px 40px / 10px 20px 30px 40px; 多种写法，分别表示水平和竖直的值 
-  box-shadow: (外阴影)10px 10px 10px 10px skyblue; 水平偏移量  竖直偏移量  模糊值(高斯模糊，基于边框的原来位置向边框两边去模糊)  水平和垂直（四个）方向同时向 外增大        给盒子加阴影，外阴影和内阴影都能加，阴影在背景颜色上边，在内容下边 
-  box-shadow: (内阴影) inset 10px 10px 10px 10px skyblue;   增加是向内缩小 
-  box-shadow: (可以写多个值) 10px 10px 10px 10px skyblue,inset 10px 10px 10px 10px skyblue,10px 10px 10px 10px red,inset 10px 10px 10px 10px red;  哪 个阴影最先设置哪个阴影在最上边，设置重复的值可以加重阴影，让阴影更实一点 
-  border-image: source slice repeat; 一般这三个写一块，单独写width和outset 
-  border-image-source: (资源)url();**支持渐变色**linear-gradient(red,skyblue); 
-  border-image-slice:(截取，可以填1 - 4个值，只能填数字或百分比，分别代表top right bottom left，将图片分割成9份取用周围的8份)默认值为100%，但是只显示四个角， 最后可以加fill，把内容区也填充 
-  border-image-width: (设置border里背景图片所占的宽度，一般小于边框的宽度，一般不动它，默认值为1，填auto会与slice看齐，) 
-  border-image-outset:(使边框图片往外延伸) 
-  border-image-repeat:stretch(默认值,拉伸) | repeat(平铺，相当于复制填充，能填充多少填多少，不够一个铺半个) | round(完整平铺，先拉伸平铺，等到达一定程度压缩  平铺，不会平铺出来半个) | space(完整平铺，先拿空白铺，等一定程度加一个新的图形)  可以填两个参数 

### color

- RGB
- RGBA
- HSL(色调0360,饱和度0.0%100%,亮度)

### background

-  background: linear-gradient(渐变方向to right | to top right 可组合 | 0deg 0度,颜色,颜色长度,颜色,颜色长度 to top right | 45deg,#0f0,60px,#00f,20px, #ff0,80px)线性渐变; radial-gradient(circle圆 | ellipse椭圆,closest-corner放射半径到最近的角截止 | closest-side放射半径到最近的边截止 | farthest-corner放 射半径到最远的角截止 | farthest-side,at 100px | at top right圆心位置,#0f0,60px,#00f,20px)径向渐变; 
   - background: linear-gradient(to top,#f00,#ff0,#00f)
-  background-image: url() url() url();可以设置多张背景图片 
-  background-size: 100px 200px,100px 200px,100px,200px;给多张背景图片设置尺寸，一一对应 
-  background-position: 0 0,100px 0,200px 0;给多张背景图片设置位置，一一对应，origin是哪个，就相对于哪个定位 
-  background-origin: 设置图片打哪起始，从值的左上开始，但不从值的右下结束，默认到border结束，默认值为padding-box,有三个值，border-box;padding-box;  content-box;从这里开始，但不从这里结束 
-  background-clip: 设置图片从哪结束，四周都是边界，默认值为border-box,有四个值，border-box;padding-box;content-box;text;
   `css`
   -webkit-background-clip:text;
   background-clip: text;
   -webkit-text-fill-color: transparent;
   text-fill-color:transparent;
   `css` 
-  background-attachment: 设置图片相对位置，默认值为scroll,表示相对容器视口定位;local,相对于内容区定位，和内容并到一块;fixed,相对于浏览器视口定位，超出容器范围  不显示，也相对容器视口定位 
-  background-size:设置图片尺寸，cover,在不改变原来图片比例的前提下用一张图片完整填充内容区，比例不同会溢出容器，不可能出现两张图片，不会repeat;contain,在不改 变原来图片比例的前提下用内容区包裹完整的图片，用一条边与图片对齐，然后完整显示图片，比例不同会留白，可能出现两张图片，会repeat； 
-  background-repeat:可以填no-repeat;repeat-x;repeat-y;round(平铺，稍稍拉伸或压缩，能填新图片或减少新图片时添加或减少);space(空白填充，不会改变图片大小);
   background-repeat: round space; | space round;可以填两个值，分别代表横向纵向 

### text

-  text-shadow: x,y,blur,color;10px 10px 3px #000,-10px -10px 3px #00f;可以填多个值 
-  @font-face{引入字体包
   font-family: 'abc';给字体包起名字
   src: () format('字体后缀')强行映射;
   }
-  **固定写法**
   div{
   font-family: 'abc'; 调用字体包
   }
   - 字体包(
     truetype  微软 苹果 联合开发                     .ttf
     opentype  微软 Adobe 联合开发 基于.ttf且优于.ttf  .opt
     woff                                            .woff
     .eat
     .svg
     MIME (Multipurpose Internet Mail Extensions)多用途互联网邮件扩展类型。是设定某种扩展名的文件用一种应用程序来打开的方式类型，当该扩展名文件被访问的时候，  浏览器会自动使用指定应用程序来打开。多用于指定一些客户端自定义的文件名，以及一些媒体文件打开方式。
     ) 

#### 以下自查自用可

-  white-space 
-  word-break: keep-all不换行;break-all强制换行;break-word尽可能的保留一个英文单词的完整性; 
-  column多列 
   - columns: 宽度 列数;100px 4;
   - column-count:列数 3;
   - column-gap: 两列之间的空白宽度;30px;
   - column-rule: 1px solid black;两列之间加分割线
   - column-span: all;某段文字贯穿所有列
   - column-break-before:在某元素前另起一列
   - column-break-after:在某元素后另起一列

### box

与CSS2盒子的区别在于计算方式的不同

-  W3C Standards mode(W3C标准模式)： 原来盒子的宽度和高度等于width(内容区)+padding+border，boxWidth = width + padding(2) + border(2) 
-  IE 6 Quirks mode(IE6混杂模式)：box盒子的宽度和高度就等于width(内容区+padding+border)，boxWidth = width = comtentWidth + padding(2) + border(2) 
-  box-sizing: border-box;使盒子变为IE 6 Quirks mode 
-  overflow(溢出): 默认为visible(显示);hidden(隐藏); scroll(添加滚动条);auto(有溢出添加滚动条，没有不添加);可以有overflow-x,overflow-y;单独设置一个方向时，  另一个默认为auto 
-  resize(盒子大小用户是否可改变): 必须配合overflow属性使用，单独设置不生效，默认为none(不允许改变);both(宽度高度都可调节);horizontal(可调节宽度);vertical(可  调节高度) 
-  flex: 弹性盒子，能伸能缩 
-  设置到父级上的：
   - display: flex | inline-flex(行级块弹性盒模型);放在父级里，让父级变成一个弹性盒模型
   - flex-direction: row | column | row-reverse(倒着排) | column-reverse;设置主轴方向，默认为row，另一个轴称为交叉轴，与主轴垂直
   - flex-wrap: 设置父级元素宽度不够时排列是否换行，默认值为nowrap不换行;wrap换行;wrap-reverse倒着换行,从下边开始排;
   - justify-content: 默认值flex-start开头对齐; flex-end末尾对齐; center居中对齐; space-between两端对齐;
   - space-around平均对齐，相当于在两端加margin;
   - align-items: 基于交叉轴进行位置设置，默认值flex-start开头对齐; flex-end末尾对齐; center居中对齐;
   - baseline基于文字底线对齐; stretch没设置高度时把高度撑满
   - align-content: 基于交叉轴进行多行元素位置设置，只能应用于多行，默认值flex-start开头对齐; flex-end末尾对齐; center居中对齐; space-between两端对齐;   space-around平均对齐，相当于在两端加margin;
   - stretch没设置高度时把高度撑满 
-  设置到子元素上的：
   - order: 填数，越小越靠前，默认值为0
   - aline-self: 默认值flex-start开头对齐; flex-end末尾对齐; center居中对齐; baseline基于文字底线对齐; stretch没设置高度时把高度撑满;优先级高于父级设置的位置， 但是优先级低于align-content，集体优先
   - flex: 默认值 0 1 auto;
   - flex-grow: 填数，默认为0，当主轴方向还有剩余空间的时候，根据自己的比例瓜分剩余空间，都填1的话就是按1:1进行瓜分
   - flex-shrink: 填数，默认为0，压缩的是内容区，当主轴方向溢出的时候，根据自己真实的内容区所占长度*比例再 / 所有子元素所占总长度进行缩放，也就是占得越多缩得越多，  如多出200px，总占有1600px，比例为1:1:4,4对应300px，则为(300*4)/1600*200 = 150px;即4缩放150px 
   - **被不换行内容撑开的元素不参与压缩，可以换行参与压缩，中文可以压缩，word-break: break-word;使换行**
-  flex-basis: 设置基于主轴方向的长度，优先级高于width，如设为100px;宽度width为200px;则显示为100px;可以理解为width的取代值 
   - **只设置basis，则元素最小宽度为basis**
   - **同时设置basis和width且basis < width,则basis < realWidth < width;即basis是最小宽度，width是最大宽度，元素宽度可在两值之间根据内容长度改变**

### transition

- transition: 过渡，一般直接写，all 2s linear 1s;添加在要被改变的元素上，后两个可以不填，可以多填，width 2s, height 1s; 
  -  transition-property: all全部;属性名(有改变的属性且需要过渡的) 
  -  transition-duration: 1s;过渡时长 
  -  transition-timing-function: 默认ease平滑过渡; 过渡方式 linear线性过渡; ease-in由慢到快; ease-out由快到慢; ease-in-out由慢到快再到慢; 
     -  steps(1,start | 1,end);逐帧动画，接受两个参数的步进函数，第一个参数必须是正整数，指定函数的运行步数，填几就是几步到位，没有过渡效果，第二个参数是start或  end，start是保留下一帧的状态，直到这段动画时间结束，也就是会看不见第一帧的状态，直接从第二帧开始显示，不容易弥补缺陷; end是保留当前帧的状态，直到这段动画时间 结束，也就是会看不见最后一帧的状态，从显示着倒数第二帧直接结束，可以加forward弥补end缺陷 
     -  cubic-bezier(0.2,-1.3,0.5,1.63);三次贝赛尔曲线，填四个数值代表坐标点，1、3数字是x轴，2、4数字是y轴，x轴上两个点在区间[0,1]内取值，y轴可以小于0大于1，基 于贝塞尔方程式绘制曲线，**公式：B(t) = P₀(1 - t)³ + 3P₁t(1 - t)² + 3P₂t²(1 - t) + P₃t³ ,t ∈ [0,1]** 
  -  transition-delay:0;过多长时间执行动画，默认为0 

### animation

-  animation: name 3s, name2 4s, name3 cubic-bezier(0.2,-1.3,0.5,1.63);可以写多个，并行执行，填贝塞尔曲线会改变每一段的运动状态，但每一段运动状态都一样 

```css
@keyframes  name{ 
0%{ //0%可以用from代替
left:100px;
top:100px;
background-color: red;
}
50%{
left:0;
top:100px;
background-color: yellow;
}
100%{ //100%可以用to代替
left:0;
top:0;
background-color: blue;
}
}; 
```

-  @keyframes: 关键帧容器，加一个关键帧名字,里边填关键帧元素状态 
-  animation-name: name;填关键帧名字 
-  animation-duration: 3s;过渡时长 
-  animation-timing-function: 默认ease平滑过渡; 过渡方式 linear线性过渡; ease-in由慢到快; ease-out由快到慢; ease-in-out由慢到快再到慢; 
-  animation-delay:0;过多长时间执行动画，默认为0 
-  animation-iteration-count: 默认值1;规定动画运行次数，infinity无限运动 
-  animation-direction: 默认值为normal;reverse跟据关键帧倒着运动;alternate先正着执行一次再倒着执行一次，iteration必须大于等于2;alternate-reverse第一次开始 先倒着执行，再正着执行 
-  animation-play-state:running运动;paused停止;可配合伪元素使用，不常用 
-  animation-fill-mode: 默认为none不设置动画对象之外的状态; forwards设置对象运动之后的状态为动画结束时的状态，也就是最后一帧的状态; backwards设置对象运动开  始之前的状态为动画开始时的状态，也就是第一帧的状态; both设置对象开始之前和运动之后的状态为动画结束或开始的状态; 
-  animation: name 3s cubic-bezier(0.2,-1.3,0.5,1.63) 1s both; 

####  css动画和js动画的区别

- js 动画代码相对复杂，一些动画运行时，对动画的控制程度上
  - js 能够让动画，暂停，取消，终止
  - css动画不能添加事件
- 动画性能上
  - js 动画多了一个js 解析的过程，性能不如 css 动画好

### transform{}的属性

-  rotate(角度值 90deg | 弧度值 1rad | 圈 1turn | 梯度值 100grad);水平旋转,旋转中心为元素中心,类似Z轴
   **元素旋转的时候元素参照的坐标轴也跟着旋转** 
-  transform-origin: 设置中心,默认值为 center center; 给谁设相当于参照谁，比如 0 0;是设旋转中心为左上角 
-  rotateX(角度值 90deg | 弧度值 1rad | 圈 1turn | 梯度值 100grad) 
-  rotateY(角度值 90deg | 弧度值 1rad | 圈 1turn | 梯度值 100grad) 
-  rotateZ(角度值 90deg | 弧度值 1rad | 圈 1turn | 梯度值 100grad) 
-  rotate3d(x,y,z,angle角度);以(x,y,z)坐标点为目标点，从原点到此点为矢量方向，按此矢量方向进行旋转 
-  scale(x,y);沿着x轴y轴对元素进行扩大或缩小，默认值为(1,1);伸缩的是元素所在坐标轴的刻度，使刻度增大减小，引起视觉上的伸缩，元素实际尺寸没有变化
   transform: scale(0.5,0.5) scale(3,3);可叠加操作，后一个按照前一个伸缩后的刻度伸缩
   **所有伸缩过的方向影响会一直被保留，也就是这一刻的伸缩轴被固定在了此处，这一刻的伸缩影响不会跟着旋转，但伸缩轴依然跟着旋转，只是当元素旋转后会按着原来的伸缩方向  伸缩，而不是跟着伸缩轴的新方向伸缩** 
   - scalex()单方向伸缩
   - scaley()单方向伸缩
   - scalez()单方向伸缩
   - scale3d()设置伸缩方向，从原点到此目标点为矢量方向
-  skew(x,y);倾斜的是坐标轴，倾斜的同时伸缩坐标值，使水平方向和竖直方向的视觉大小不变 
-  translate(x,y); 
-  translayex(); 参考自身按x轴平移，可用100%表示自身长度，如translatex(50%),表示向x方向平移自身长度的一半,坐标轴跟着一块平移 
-  translatey(); 参考自身按y轴平移，可用100%表示自身长度，如translatey(50%),表示向y方向平移自身长度的一半,坐标轴跟着一块平移 
-  translatez(); 参考自身按z轴平移，可用100%表示自身长度，如translatez(50%),表示向z方向平移自身长度的一半,坐标轴跟着一块平移 
-  translate3d(x,y,z,长度); 按原点到此目标点的矢量方向平移 
-  transform: perspective();添加到子元素上的景深效果，在每个元素自身上加一个眼睛，需要填在transform属性值的最前边 
-  transform-style: 默认值为平面显示flat; 3D显示 preserve-3d;应在直接父级上加，只对子元素有用，孙子元素也没法继承 
-  backface-visibility: hidden 隐藏元素背面显示，使元素转到背面不可见; 

#### matrix,矩阵是transform给咱们选中的计算规则

- matrix(1,0,0,1,e,f) === translate(x,y)

### perspective，添加到父元素上的景深效果，给父元素添加一个眼睛去看所有子元素

-  perspective: 景深，视点离元素的距离，增加立体感空间感，默认值为none; 值为[1 - infinity];
   - **视点实际看到的是物体在屏幕上的投影，没有translatez的时候不管perspective的值是多少元素的视觉大小不变，当translatez为正也就是在屏幕之前，perspective的值越大  元素视觉上增大的就越小，perspective的值越小元素视觉上增大的就越多；当translatez为负也就是在屏幕之后，perspective的值越大元素视觉上减小的就越小，perspective 的值越小元素视觉上减小的就越多** 
-  perspective-origin: 默认值center center; 视角位置，可以填空间的，不只是平面的
   - perspective-origin: 100px 100px 100px; 分别表示x y z,如果元素长宽高是200px，现在就代表把视点添加在元素的立体中心 

## 性能优化

- CPU：整型
- GPU：浮点型
- 浏览器下载顺序：download html     --        download css       --          download js --
  css rules tree(construct)                donAPI
  domTree

```
                                  cssrulestree                           cssomAPI
                                                                         cssomTree

                                  domtree                                cssomTree

                                                      renderTree

                                                           |
                                                           |

                                                        layout  ----->   paint
                                                      (reflow)            (repaint)
                                                         逻辑图(多层矢量图) 
                                                         实际绘制(栅格化)

                                                         reflow比repaint耗性能
```

- 引起reflow(重排)：
  - 改变窗口大小
  - 改变文字大小
  - 内容的改变，输入框输入文字
  - 激活伪类
  - 操作class属性
  - 脚本操作DOM
  - 计算offsetWidth和offsetHeight
  - 设置style属性
- 引起repaint(重绘)：
  - 只是修改某某一元素的字体颜色大小等内容
  - 一般浏览器刷新页面的频率为 1s 60次  也就是60fps
  - 大概16.7ms一次
  - 如果GPU可以在一帧里渲染好页面，则改动页面的元素或实现动画的时候，将会非常流畅

### will-change:  提前告诉浏览器某个属性用GPU渲染

```css
will-change: transform;
div:hover{
will-change: transform;
}
div{
transform: ;
}
```

## 显示器的成像原理及px的实际意义

### 空间混色法

- RGB 光学三原色在空间上的混合方法，三原色构成一个像素点，品字型或柱状型

### 显示屏

-  crt显示屏，求点距的方法的意义的 
-  LCD液晶屏 LED液晶屏 

### 像素px

- 点距可以代表像素大小，但不是实际像素大小，等边三角形等边点距，等腰三角形水平点距，三个点空间混合法
  - 栅格型点距，三条空间混合法
  - 像素说到底是相对单位
  - 物理像素  ===  设备出厂时，像素的大小
- DPI  一英寸所能容纳的像素点数  1 in = 2.54cm
  - 960DPI = 2.54 / 100 = 0.25mm
  - 200DPI ≈ 0.10mm | 0.15mm
  - dpi = ppi
  - dpi 最早形容打印机在一英寸的屏幕里可以打印多少个墨点
  - ppi 一英寸所能容纳的像素点数(点距数)
- 参照像素
  - 标杆：以96dpi的显示屏 一臂距离的视角去看，显示出的具体大小  1/96 * 英寸  其他的dpi的显示屏显示的大小都跟着96的大小保持一致
  - 标杆也称为css像素，也叫做逻辑屏幕
  - css像素 = 逻辑像素
  - 分辨率表示在固定宽高下展示的像素点数
  - 设备像素比  dpr = 物理像素 / css像素 

### 响应式

- 响应式网页设计或称自适应网页设计或称回应式网页设计/对应式网页设计，是一种网页设计的技术做法，该设计可使网站在不同的设备（从桌面计算机显示器到移动电话或其他移动产 品设备）上浏览时对应不同分辨率皆有适合的呈现，减少用户进行缩放，平移和滚动等操作行为。
- 真正的响应式设计方法不仅仅是根据可视区域大小而改变网页布局，而是要从整体上颠覆当前网页的设计方法，是针对任意设备的网页内容进行完美布局的一种显示机制。
- 只需要开发一套页面，让用户在不同的设备上(不管大小或分辨率如何改变)看到的页面呈现效果是完美的
- width=device-width：iphone或者iPad上横竖屏的宽度 = 竖屏时的宽度
- initial-scale=1.0 ： windows iphone ie浏览器上横竖屏的宽度 = 竖屏时的宽度
- 模拟移动端的meta：
  - width： 可视区宽度
  - device-width:  设备宽度
  - minimum-scale： 最小缩放比
  - maximum-scale： 最大缩放比
  - user-scalable： 是否允许用户缩放
- Css像素根据设备像素进行计算  1css 像素  == 1 设备像素    设备的分辨率  dpi值来计算css像素真正展现的大小
- 适配各种不同分辨率的设备

#### 实现响应式

-  流体网格：可伸缩的网格 (大小宽高  都是可伸缩(可用flex或者百分比来控制大小)float) ---> 布局上面 元素大小不固定可伸缩 
-  弹性图片：图片宽高不固定(可设置min-width: 100%) 
-  媒体查询：让网页在不同的终端上面展示效果相同(用户体验相同 ---> 让用户用着更爽) 在不同的设备(大小不同 分辨率不同)上面均展示合适的页面
-  **媒体查询不占用权重，一般会把媒体查询放在最后，放在前边容易被覆盖**
-  媒体查询是向不同设备提供不同样式的一种方式，它为每种类型的用户提供了最佳的体验。css2: media typemedia type(媒体类型)是css 2中的一个非常有用的属性，通过 media type我们可以对不同的设备指定特定的样式，从而实现更丰富的界面。css3: media querymedia query是CSS3对media type的增强，事实上我们可以将media query 看成是media type+css属性(媒体特性Media features)判断。 
   -  如何使用媒体查询？
      - 媒体查询的引用方法有很多种：
        - link标签：
          [@import ](/import ) url(example.css) screen and (width:800px); 
          css3新增的[@media ](/media )  
        - 媒体类型（Media Type): 
          - all(全部)
          - screen(屏幕)
          - print(页面打印或打印预览模式）

![image.png](./images/CSS3学习/1.png)

         - 媒体特性（Media features): 
            - width(渲染区宽度)
            - device-width(设备宽度)...
            - Media Query是CSS3 对Media Type的增强版，其实可以将Media Query看成Media Type(判断条件)+CSS(符合条件的样式规则) 

![image.png](./images/CSS3学习/2.png)

   -  逻辑运算：
      - 合并多个媒体属性 and
        [@media ](/media ) screen and (min-width: 600px) and (max-width:100px); 
        合并多个媒体属性或合并媒体属性与媒体类型, 一个基本的媒体查询，即一个媒体属性与默认指定的screen媒体类型。
        指定备用功能 
        [@media ](/media ) screen and (min-width: 769px), print and (min-width: 6in); 
        没有or关键词可用于指定备用的媒体功能。相反，可以将备用功能以逗号分割列表的形式列出
        这会将样式应用到宽度超过769像素的屏幕或使用至少6英寸宽的纸张的打印设备。
        指定否定条件 not
        [@media ](/media ) not screen and (monochrome); 
        要指定否定条件，可以在媒体声明中添加关键字not，不能在单个条件前使用not。该关键字必须位于声明的开头，而且它会否定整个声明。所以，上面的示例会应用于除单色屏幕 外的所有设备。
      - 向早期浏览器隐藏媒体查询 only
        media="only screen and (min-width: 401px) and (max-width: 600px)";
        媒体查询规范还提供了关键字only，它用于向早期浏览器隐藏媒体查询。类似于not，该关键字必须位于声明的开头。Only指定某种特定的媒体类型  为了兼容不支持媒体查询的  浏览器
        早期浏览器应该将以下语句media="screen and (min-width: 401px) and (max-width: 600px)";
        解释为media="screen"; 换句话说，它应该将样式规则应用于所有屏幕设备，即使它不知道媒体查询的含义。
        无法识别媒体查询的浏览器要求获得逗号分割的媒体类型列表，规范要求，它们应该在第一个不是连字符的非数字字母字符之前截断每个值。所以，早期浏览器应该将上面的示例 解释为：media="only"
        因为没有only这样的媒体类型，所以样式表被忽略
        Query --> css3 
   -  主要断点： 设备宽度的临界点 

![image.png](./images/CSS3学习/3.png)

      - 大小的区别 ---> 宽度不同   ---> 根据不同宽度展示不同的样式
      - 响应式网页开发主要是在css样式上面进行操作
         -  易混淆的宽度 device-width/height

width/height来做为的判定值。
device-width/device-height 是设备的宽度（如电脑手机的宽度 不是浏览器的宽度）
width/height使用documentElement.clientWidth/Height即viewport的值。渲染宽度/高度
视口宽度/ 

### 单位

- rem：rem是CSS3新增的一个相对单位（root em，根em）相对的只是HTML根元素font-size大小。
- em：em是相对长度单位。相对于当前对象内文本的字体尺寸font-size大小。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。
- px： px像素（Pixel）。相对长度单位。像素px是相对于显示器屏幕分辨率而言的。
- vw：相对于视口的宽度。视口被均分为100单位的vw, 会把视口分成100份
- vh：相对于视口的高度。视口被均分为100单位的vh, 会把视口分成100份
- vmax： 相对于视口的宽度或高度中较大的那个。其中最大的那个被均分为100单位的vmax
- vmin：相对于视口的宽度或高度中较小的那个。其中最小的那个被均分为100单位的vmin

### 响应式不一定是最佳选择

内容设计问题都可以通过响应式设计思路解决， 项目的预算，目标用户以及定位决定了其实现方式。
项目的预算，人力，物力，财力， 时间成本
目标用户，
产品定位

- 渐进增强 --->  iphone6 向上兼容  兼容最新设备
- 优雅降级 --->  开发通用版本  再兼容老版本   向下兼容
- 先移动端  ---> pc端
- 先iphone6为初始原型 开发  ---> 兼容其他的设备  --->  渐进增强

## ios滑动卡顿 

-  -webkit-overflow-scrolling:touch 可能会在IOS系统低的情况出现滚动条；尝试溢出解决