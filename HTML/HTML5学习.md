# [HTML5](https://developer.mozilla.org/zh-CN/docs/Web/CSS)
## 属性篇

-  placeholder	输入框的提示信息
-  input的type，应用于form表单下的 
   - Calendar类 
     -  date 日期选择，丑，兼容性不好，一般都是使用js制作日期框， 
     -  time 选择时间，上下午 
     -  week 选择周 
     -  datetime-local 综合选择日期，年月日 + 时间 
     -  number 限制只能输入数字  
     -  email 限制输入邮箱格式  
     -  color 选择颜色  
     -  range 可拖动的进度条，设置最大最小值：  
     -  search 会记录历史输入的输入框，在下拉列表中提示   
     -  url 限制只能输入url格式  
     -  submit 提交数据给接收地址 
-  contenteditable  将文本改为输入框，在页面上可以修改，可继承
   - 默认值false，不可修改，true会将文字改为一个文本框，可在页面上进行修改，可以将整个标签都删除，尽量不要嵌套使用 
-  draggable 使属性盒子可以拖拽 
   - 在 HTML5 中，拖放是标准的一部分，任何元素都能够拖放
   - 默认值为false，true是可拖拽，拖拽出一个虚影，松手回到原位置，a标签、img标签默认可拖拽 
   - 拖拽的声明周期，拖拽的组成： 
     - 拖拽开始，拖拽进行中，拖拽结束
     - 被拖拽的物体，目标区域（目标元素）
   - 事件是由行为触发的，但是一个行为可以不止触发一个事件
   - **所有的标签元素，当拖拽周期结束时，默认事件是回到原处**

```js
var dom = document.querySelector(".div")
dom.ondragstart = function(e){ 
  e.dataTransfer.effectAllowed = 'link' | 'copy' | 'move';//改变鼠标拖拽时的指针，只在ondragstart下设置才能生效          
  // 移动开始瞬间触发的事件      
}
dom.ondrag = function(e){ 
  // 移动进行中触发的事件      
}
dom.ondragend = function(e){
  // 移动结束瞬间触发的事件
} 
var target = document.querySelector(".target");
target.ondragenter = function (e) {
  // 当鼠标带着被拖拽物体移入(鼠标移入)目标区域时触发的事件
}
target.ondragover = function(e){
  //当鼠标带着被拖拽物体移入目标区域并松手后触发的事件
  //ondragover --> 回到原处 -->执行ondrop事件
}
target.ondragleave = function(e){
  //当鼠标带着被拖拽物体移入目标区域再移出后触发的事件
}
target.ondrop = function(e){
  e.dataTransfer.dropEffect = 'link';//改变鼠标松开时的指针，只在ondrop下设置才能生效
  //当移动事件结束后默认触发的事件，但不会触发，阻止ondragover事件后才触发
}
```

## 语义化标签，带有不同含义的div

```html
<header></header> // 头部区域
<footer></footer> // 底部区域
<nav></nav> // 导航栏
<article></article> // 整篇文章
<section></section> // 段落
<aside></aside> // 侧边栏
```

## canvas

- **像素图，适合用于小面积的绘图，适合动画，用标签和js去画**
- **VSCode中无法提示canvas内容**
- `[**_@type _**](/type )**_ {HTMLCanvasElement}_**`**将上述代码添加到获取的canvas对象上方即可**
  - **@type可以指定获取对象的类型【此处指定HTMLCanvasElement类型】**
  - **此时编辑器就可以进行自动提示了**
- 画线

```html
<script>
    var can = document.getElementById("can");
    var ctx = can.getContext("2d"); // 设置为2d画布, .getContext() 方法返回canvas 的上下文，如果上下文没有定义则返回 null
    ctx.lineWidth = 5; // 设置画笔宽度为5 
    ctx.moveTo(100, 100); // 设置起点
    ctx.lineTo(200, 100); // 设置终点
    ctx.stroke(); //渲染
    ctx.beginPath(); //重新开启路径
    ctx.lineWidth = 2;
    ctx.moveTo(200, 100);
    ctx.lineTo(200, 200);
    ctx.lineTo(300,200);
    ctx.closePath(); // 闭合同一路径下的线
    ctx.fill(); // 填充为实体
    ctx.strokeStyle = 'red'; //线的颜色改为red
    ctx.fillStyle = 'blue'; //填充颜色为blue
    ctx.clearRect(0,0,400,300);//清除画布中的内容，从(0,0)坐标到(400,300)坐标
    ctx.stroke(); 
</script>
```

- 画矩形

```html
 <script>//画矩形
     var can = document.getElementById("can");
     var ctx = can.getContext("2d"); // 设置为2d画布
     ctx.lineWidth = 5; // 设置画笔宽度为5 
     ctx.rect(100,100,200,50); // 构建矩形路径，分别代表矩形左上角的坐标和矩形长宽
     ctx.stroke();
     ctx.strokeRect(120,120,200,100); // 构建矩形路径并渲染
     ctx.fillRect(150,150,80,40); // 构建矩形路径并填充渲染
 </script>
```

- 画圆

```html
<script>//画圆
    var can = document.getElementById("can");
    var ctx = can.getContext("2d"); // 设置为2d画布
    ctx.lineWidth = 2; // 设置画笔宽度为5 
    ctx.arc(100,100,50,0,Math.PI,1);//圆心(100,100)，半径50，弧度(起始弧度0，结束弧度π)，方向(顺时针0，逆时针1)
    ctx.fill(); 
    ctx.stroke();
</script>
```

- 画圆角矩形

```html
<canvas id="can" width="400px" height="300px"></canvas>
<script>//画圆角矩形
  var can = document.getElementById("can");
  var ctx = can.getContext("2d"); // 设置为2d画布
  ctx.moveTo(100,105);
  ctx.arcTo(100,200,200,200,5); //设置终点位置(100,200)和圆弧方向(200,200)及线的像素5
  ctx.arcTo(200,200,200,100,5);
  ctx.arcTo(200,100,100,100,5);
  ctx.arcTo(100,100,100,200,5);
  ctx.fill();
  ctx.stroke();
</script>
```

- 画二次样条曲线

```html
<script>//画二次样条曲线
    var can = document.getElementById("can");
    var ctx = can.getContext("2d");
    var height = 300,
        width = 400,
        offect = 0,
        num = 0;
    var timer = setInterval(function(){
    ctx.clearRect(0,0,400,300);
    ctx.lineWidth = 2; // 设置画笔宽度为5 
    ctx.beginPath();
    ctx.moveTo(0 + offect - 400,height / 2);
    ///贝赛尔曲线，控制点横坐标，控制点纵坐标，二次样条曲线终点的横坐标，二次样条曲线终点的纵坐标
    ctx.quadraticCurveTo(width / 4 + offect - 400, height / 2 + Math.sin(num) * 120, width / 2 + offect - 400, height / 2);
    ctx.quadraticCurveTo(width / 4 * 3 + offect - 400, height / 2 - Math.sin(num) * 120, width + offect - 400, height / 2);

    ctx.quadraticCurveTo(width / 4 + offect, height / 2 + Math.sin(num) * 120, width / 2 + offect, height / 2);
    ctx.quadraticCurveTo(width / 4 * 3 + offect, height / 2 - Math.sin(num) * 120, width + offect, height / 2);
    offect += 5;
    offect %= 400;
    num += 0.01;
    ctx.stroke();
    },1000/30)
</script>
```

- 绘制贝塞尔曲线

```html
<script>//绘制贝塞尔曲线
    var can = document.getElementById("can");
    var ctx = can.getContext("2d");  
    ctx.fillStyle = "#eeeeff";
    ctx.fillRect(0,0,500,400)
    var n = 0,
        dx = 150,
        dy = 150,
        s = 100;
    ctx.beginPath();
    ctx.globalCompositeOperation = 'and';
    ctx.fillStyle = 'rgb(100,255,100)';
    var x = Math.sin(0),
        y = Math.cos(0),
        dig = Math.PI / 15 * 11;
    ctx.moveTo(dx,dy);
    for(var i = 0;i < 30; i++){
        var x = Math.sin(i * dig),
            y = Math.cos(i * dig);
            //第一个控制点的横坐标，第一个控制点的纵坐标，第二个控制点的横坐标，第二个控制点的纵坐标，曲线终点的横坐标，曲线终点的纵坐标
        ctx.bezierCurveTo(dx + x * s, dy + y * s - 100, dx + x * s + 100, dy + y * s, dx + x * s, dy + y * s);
    }
    ctx.closePath();
    ctx.fill();
    ctx.stroke();
</script>
```

- 旋转缩放，保存还原

```html
 <script>//旋转缩放，保存还原
     var can = document.getElementById("can");
     var ctx = can.getContext("2d");
     ctx.save(); // 保存当前的坐标系状态，以及平移数据、缩放数据、旋转数据
     ctx.beginPath();
     ctx.translate(100,100); // 改变画布坐标系原点的位置
     ctx.rotate(Math.PI / 6); // 旋转默认原点是画布坐标系原点，旋转30度
     ctx.moveTo(0,0);
     ctx.lineTo(100,0);
     ctx.stroke();
     ctx.restore(); // 还原保存的数据
     ctx.beginPath();
     ctx.translate(50,50);
     ctx.scale(2,2); // 所有属性值扩大2倍，包括xy坐标值，及距离画布边的距离，还有边长
     ctx.strokeRect(80,60,80,60);
 </script>
```

- 背景填充

```html
 <script>//图片填充
     var can = document.getElementById("can");
     var ctx = can.getContext("2d");
     var img = new Image();
     img.src = "../照片册/images/1.jpg";
     img.onload = function(){
         ctx.beginPath();
         ctx.translate(100,100);
         var bg = ctx.createPattern(img, "no-repeat"); // 创建背景图片
         ctx.fillStyle = bg; // 内容填充为图片
         ctx.fillRect(0,0,800,600);
     }
 </script>
 <script>//线性渐变
     var can = document.getElementById("can");
     var ctx = can.getContext("2d");
     ctx.beginPath();
     ctx.translate(100,100);
     var bg = ctx.createLinearGradient(0, 0, 800, 600); //线性渐变，渐变起始点也是从画布原点开始，填入渐变起始点坐标(0,0)，终点坐标(800,600)
     bg.addColorStop(0, 'skyblue'); //添加渐变颜色关键帧，只能是0 - 1之间的数字
     bg.addColorStop(0.5, '#ff0'); 
     bg.addColorStop(1, '#f00');
     ctx.fillStyle = bg; //把线性渐变插入绘制的图形中
     ctx.fillRect(0,0,800,600);
 </script>
 <script>//辐射渐变
     var can = document.getElementById("can");
     var ctx = can.getContext("2d");
     ctx.beginPath();
     ctx.translate(100,100);
     var bg = ctx.createRadialGradient(200,200,10,200,200,200) //辐射渐变，两个圆，分别填第一个圆的圆心和半径(200,200,10)，第二个圆的圆心半径(200,200,200)，渐变是从第一个圆的边开始的
     bg.addColorStop(0, 'skyblue'); //添加渐变颜色关键帧，只能是0 - 1之间的数字
     bg.addColorStop(0.5, '#ff0'); 
     bg.addColorStop(1, '#f00');
     ctx.fillStyle = bg; //把线性渐变插入绘制的图形中
     ctx.fillRect(0,0,800,600);
 </script>
```

- 添加阴影

```html
<script>//添加阴影
    var can = document.getElementById("can");
    var ctx = can.getContext("2d");
    ctx.beginPath();
    ctx.shadowColor = 'red'; // 设置阴影颜色
    ctx.shadowBlur = 60; // 设置阴影大小
    ctx.shadowOffsetX = 30; // 设置阴影水平偏移量，正常是平分于线两端
    ctx.shadowOffsetY = 30; // 设置阴影竖直偏移量
    ctx.fillRect(100,100,600,400);
</script>
```

- 设置字体

```html
<script>//设置字体
    var can = document.getElementById("can");
    var ctx = can.getContext("2d");
    ctx.beginPath();
    ctx.font = '60px Georgia'; // 设置字体大小和字体
    ctx.strokeText('啦啦啦', 200, 200); // 字体描边
    ctx.fillStyle = 'skyblue'; // 设置填充颜色
    ctx.fillText('哈哈哈', 400, 400); // 字体填充
</script>
```

- 两端线头和相交线端样式

```html
<script>//两端线头和相交线端样式
    var can = document.getElementById("can");
    var ctx = can.getContext("2d");
    ctx.beginPath();
    ctx.lineWidth = 15;
    ctx.moveTo(100,100);
    ctx.lineTo(200,100);
    ctx.lineTo(100,150);
    ctx.lineCap = 'round';//值还有butt(原始默认样式)，square(两头加方块)，round(两头加圆角)
    ctx.lineJoin = 'miter';//值还有bevel(相交部分剪切)，miter(miterLimit)(相交部分保持默认尖端样子，或短点的尖端),round(相交部分倒圆角)
    ctx.miterLimit = 5;//相交部分保持默认尖端，但尖端长度为5
    ctx.stroke();
</script>
```

## svg

**矢量图，适合大面积的贴图，通常动画较少或者较简单，用标签和css去画**

- SVG 指可伸缩矢量图形 (Scalable Vector Graphics)
- SVG 用来定义用于网络的基于矢量的图形
- SVG 使用 XML 格式定义图形
- SVG 图像在放大或改变尺寸的情况下其图形质量不会有所损失
- SVG 是万维网联盟的标准
- SVG 与诸如 DOM 和 XSL 之类的 W3C 标准是一个整体
- 与其他图像格式相比，使用 SVG 的优势在于：
  - SVG 可被非常多的工具读取和修改（比如记事本）
  - SVG 与 JPEG 和 GIF 图像比起来，尺寸更小，且可压缩性更强。
  - SVG 是可伸缩的
  - SVG 图像可在任何的分辨率下被高质量地打印
  - SVG 可在图像质量不下降的情况下被放大
  - SVG 图像中的文本是可选的，同时也是可搜索的（很适合制作地图）
  - SVG 可以与 Java 技术一起运行
  - SVG 是开放的标准
  - SVG 文件是纯粹的 XML

- 画线和矩形，画圆、椭圆、折线，画多边形、文字

```html
<style>
  svg{
    width: 600px;
    height: 600px;
    position: absolute;
    top: calc(50% - 300px);
    left: calc(50% - 300px);
    border: 1px solid sienna;
  }
  .line{
    stroke-width: 10px;
  }
  .line1{
    stroke: sienna;<!--渲染，线的颜色-->
  }
  .line2{
    stroke: slateblue;
  }
  .line3{
    stroke: seagreen;
  }
  .line4{
    stroke: sandybrown;
  }
  .rect1{
    stroke: salmon;<!--渲染，边框的颜色-->
    fill: skyblue;<!--内部填充的颜色，默认为黑色-->
  }
  .circle1{
    fill: transparent;
    stroke: yellowgreen;
  }     
  .ellipse{
    fill: darkorange;
    stroke: darkorchid;
  }
  .polyline1{
    fill: transparent;<!--不填充-->
    stroke: yellow;
    stroke-width: 5px;<!--边框的宽度-->
    stroke-opacity: 0.6;<!--边线透明度-->
    fill-opacity: 0.5;<!--内容透明度-->
    stroke-linecap: round;<!--线头倒圆角等-->
    stroke-linejoin: round;<!--两线交点倒圆角等-->
  }  
  .polygon1{
    fill: transparent;
    stroke: yellow;
    stroke-width: 5px;
  }
  .text1{
    stroke: aqua;
    stroke-width: 2px;
  }
  .path1{
    stroke: seagreen;
    fill: transparent;
  }
  .path2{
    stroke: hotpink;
    fill: transparent;
  }
  .path3{
    fill: transparent;
    stroke: lightcoral;
  }
  .line5{
    stroke: salmon;
    stroke-width: 10px;
    stroke-dasharray: 10px 20px 30px 20px 10px;<!--将直线改为虚线，定义虚线的每段长度\(空白也算一段\)-->
  }
  .line6{
    stroke: salmon;
    stroke-width: 10px;
    stroke-dasharray: 200px;<!--将直线改为虚线，每段200px长，每两段之间的间距也是200px-->
    stroke-dashoffset: 200px;<!--将线段左移200px-->
    animation: move 2s linear infinite alternate-reverse;
  }
  @keyframes move{
    0%{
      stroke-dashoffset: 200px;
    }
    100%{
      stroke-dashoffset: 0px;
    }
  }
</style>
<body>
  <svg viewBox="0,0,300,300"><!--比例尺，改变画面比例，起点坐标，改变之后的画布大小，图像大小不变画布改变，这里是画布缩小为原来的一半，使图像看起来增大一倍-->
    <line x1="0" y1="0" x2="200" y2="200" class="line line1"></line> <!--画线，起点坐标，终点坐标-->
    <line x1="200" y1="200" x2="400" y2="200" class="line line2"></line>
    <line x1="400" y1="200" x2="200" y2="400" class="line line3"></line>
    <line x1="200" y1="400" x2="400" y2="600" class="line line4"></line>
    <rect height = "100" width = "200" x = "50" y = "50" rx = "16" ry = "30" class="rect1"></rect><!--画矩形，长宽，左上角坐标，水平方向倒圆角，竖直方向倒圆角，倒圆角只设置一个两个方向都倒，默认填充无边框-->
    <circle r = "50" cx = "200" cy = "200" class="circle1"></circle><!--画圆，半径，圆心坐标，默认填充无边框-->
    <ellipse rx = "60" ry = "40" cx = "300" cy = "300" class="ellipse"></ellipse><!--画椭圆，长半径，短半径，圆心坐标，默认填充无边框-->
    <polyline points = "0 0, 50 50, 100 200, 120 50, 180 300" class="polyline1"></polyline><!--画折线，起点坐标，中点坐标，终点坐标，默认不闭合填充无边框-->
    <polygon points="0 100, 50 150, 100 300, 120 150, 180 400" class="polygon1"></polygon><!--画多边形，起点坐标，中点坐标，终点坐标，默认闭合填充无边框-->
    <text x="200" y="50" class="text1">龙哥身体好</text>
    <path d= "M 100 100 L 200 100 l 250 150 H 300 V 50 z" class="path1"></path><!--M就是moveTo，L就是lineTo，大写代表绝对坐标，小写代表相对距离，默认不闭合填充无边框-->
    <path d="m 100 100 l 200 200 h 50 v 50 h -100 v -50 Z" class="path2"></path><!--H表示水平方向，V代表竖直方向，大写代表绝对坐标，小写代表相对距离，z表示闭合，不分大小写-->
    <path d="M 100 100 A 100 50 70 0 1 200 200" class="path3"></path><!--A表示画弧，M是起点，100 50分别是长半径短半径 70是图形顺时针旋转角度 0代表两点确定两圆的短边圆弧(改为1代表长边)，之后的1代表两点确定两圆的右边的圆(改为0代表左边的)，200 200是圆弧终点-->
    ![path画弧图片参考](Img/path画弧.jpg)
    <line x1="100" y1="500" x2="600" y2="500" class="line5"></line>
    <line x1="200" y1="400" x2="400" y2="400" class="line6"></line>
  </svg>
</body>
```

- 定义

```html
<defs><!--定义方法，类似于函数方法-->
  <linearGradient id="bg1" x1="0" y1="0" x2="100%" y2="100%"><!--线性渐变，起始位置，结束位置-->
    <stop offset="0%" style="stop-color: aqua;"></stop><!--渐变关键帧-->
    <stop offset="50%" style="stop-color:blueviolet;"></stop>
    <stop offset="100%" style="stop-color: skyblue;"></stop>
  </linearGradient>
  <filter id="Gauss1"><!--滤镜，有多个，用的时候查表-->
    <feGaussianBlur in="SourceGraphic" stdDeviation="10"></feGaussianBlur><!--高斯模糊滤镜-->
  </filter>
</defs>
<rect x="100" y="100" height="200" width="200" style="fill: url(#bg1); filter: url(#Gauss1)"></rect><!--调用方法-->
```

## video和audio

## 一些API

### 获取地理位置

- 获取地理信息，但是一些系统不支持这个功能，台式机几乎没有GPS，笔记本绝大多数也没有，智能手机几乎都有；网络也可以用来粗略估计地理位置
- 在https、file协议下可以获取，在http协议下不能获取
- 经纬度：经度最大180，维度最大90

```js
window.navigator.geolocation.getCurrentPosition(function (position) {
    console.log('成功获取', position);
}, function () {
    console.log('获取失败');
})
```

### 陀螺仪，体感

- 苹果设备的页面只有在https协议的情况下才能使用这些接口， 苹果11.x及之前的版本可以使用
- alpha：指北（指南针），[0 - 360]，0的时候指北，180的时候指南
- beta：平放时beta值为0，手机短边接触桌面立起来，下边直立时为90，倒着上边立起来为-90
- gamma：平放的时候gamma值为0，手机右长边接触桌面立起来，直立时为90，左长边立起来为-90

```js
window.addEventListener('deviceorientation', function (event) {
    document.getElementById('main').innerHTML = 'alpha:' + event.alpha + '<br/>' + 'beta' + event.beta + '<br/>' + 'gamma' + event.gamma;
})
```

### 加速度

- 加速度，acceleration，三个方向

```js
window.addEventListener('devicemotion', function(event){
    document.getElementById('main').innerHTML = event.acceleration.x + '<br/>' + event.acceleration.y + '<br/>' + event.acceleration.z;
    if(Math.abs(event.acceleration.x) > 9 || Math.abs(event.acceleration.y) > 9 || Math.abs(event.acceleration.z) > 9){
        alert('在晃');
    }
})
```

### 动画优化

```js
let timer = null;
timer = requestAnimationFrame();//每秒60帧，可传移动函数，看起来更加流畅，可以准时执行每一帧，setInterval(1000/16)的话每帧的时间少于1/60秒，兼容性极差
cancelAnimationFrame(timer);//清除requestAnimationFrame
```

### 数据存储

- coolie: 每次请求的时候都有可能传送许多无用的信息到后端，发送请求时会把所有数据带出去，存储内容较少，一般少于4k
- localStorage：只能存储字符串，长期存储的数据，无论页面是否关闭都要存储；在发送请求的时候不会把数据发出去，可以存放较多内容，5M左右
- sessionStorage：临时会话需要存储的信息，每次窗口关闭都会自动清空
- 相同协议、相同域名、相同端口才成为一个域

```js
localStorage.name = 'DaLong';
localStorage.arr = JSON.stringify([1,2,3]);
console.log(JSON.parse(localStorage.arr));
localStorage.obj = JSON.stringify({
    name: 'DaLong',
    age: 18
});
console.log(JSON.parse(localStorage.obj));

sessionStorage.name = 'DaLong';
```

### history

```html
<input type="text" id="search"><button onclick="search()">搜索</button>
<div id="main"></div>
<script>
    let data = [{
        name: 'dalong'
    }, {
        name: 'xiaobei'
    }, {
        name: 'san'
    }, {
        name: 'sier'
    }];

    function search() {
        let value = document.getElementById('search').value;
        let result = data.filter(function (obj) {
            if (obj.name.indexOf(value) > -1) {
                return obj;
            }
        });
        render(result);
        history.pushState({  //记录url，第三个参数就是锚点，hash值
            inpVal: value
        }, null, '#' + value);
    }

    function render(renderDate) {
        let content = "";
        for (let i = 0; i < renderDate.length; i++) {
            content += '<div>' + renderDate[i].name + '</div>';
        }
        document.getElementById('main').innerHTML = content;
    }
    window.addEventListener('popstate',function (e) {   //url变了就会触发
        document.getElementById('search').value = e.state.inpVal ? e.state.inpVal : " ";
        let value = document.getElementById('search').value;
        let result = data.filter(function (obj) {
            if (obj.name.indexOf(value) > -1) {
                return obj;
            }
        });
        render(result);
    })
    render(data);

    window.addEventListener('hashchange',function(e){ //hash值变了及锚点变了hashchange就会变
        console.log(e);
    })
</script>
```

### worker

- js都是单线程的，但worker的多线程的，而且是真的多线程，不是伪多线程，worker不能操作dom，没有window对象，不能读取本地文件，但可以发ajax和计算
- 理论上在worker可以继续创建worker，但实际上没有任何一款浏览器支持

```js
 let beginTime = Date.now();
 console.log('======')
 console.log('======')
 console.log('======')
 let a = 100000;
 var worker = new Worker("./worker.js");
 worker.postMessage({
     num: a
 });
 worker.onmessage = function(e){
     console.log(e.data);
 }
 console.log('======')
 console.log('======')
 console.log('======')
 let endTime = Date.now();
 console.log(endTime - beginTime);
 worker.terminate();


//worker部分代码：
importScripts("./math.js");
this.onmessage = (e) => { //接收信息
    console.log(getSum(2, 4));
    let result = 0;
    for (let i = 0; i < e.data.num; i++){
        result += i;
    }
    this.postMessage(result); //发送信息
    // this.close();  关闭worker
}


//math.js部分代码
function getSum(a, b) {
    return a + b;
}
```