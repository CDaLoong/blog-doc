!> 类是用于创建对象的模板。它们用代码封装数据以对其进行处理。JS 中的类建立在原型之上，同时还具有一些类独有的语法和语义。

!> 类的主体会执行在严格模式下，即便没有写 "use strict" 指令也一样。

## 定义类

类实际上是“特殊的函数”，就像你能够定义的函数表达式和函数声明一样，类也有两种定义方式：类表达式和类声明。

```js
// 类声明
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}

// 类表达式；类是匿名的，但是它被赋值给了变量
const Rectangle = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};

// 类表达式；类有它自己的名字
const Rectangle = class Rectangle2 {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name) // Rectangle2
```
与函数表达式类似，类表达式可以是匿名的，或者也可以有一个不同于被赋值给的变量的名称的名字。然而，不同于函数声明的是，类声明具有与 let 和 const 相同的暂时性死区限制，并且表现得像是没有被提升一样。