# ES6+

## ECMAScript、JavaScript、NodeJs 的区别

- ECMAScript：简称ES，是一个语言标准（循环、判断、变量、数组等数据类型）
- JavaScript：运行在浏览器端的语言，该语言使用ES标准。 ES + web api = JavaScript
- NodeJs：运行在服务器端的语言，该语言使用ES标准。 ES + node api = JavaScript
- 无论JavaScript，还是NodeJs，它们都是ES的超集（super set）

## ECMAScript 关键的版本

- ES3.0： 1999
- ES5.0:  2009
- ES6.0:  2015, 从该版本开始，不再使用数字作为编号，而使用年份
- ES7.0:  2016

## 为什么ES6如此重要？

ES6解决JS无法开发大型应用的语言层面的问题。

## 如何应对兼容性问题？

使用 babel 库进行版本适配就好

# 声明变量的问题

## 使用var声明变量

-  允许重复的变量声明：导致数据被覆盖 
-  变量提升：怪异的数据访问、闭包问题 
-  全局变量挂载到全局对象：全局对象成员污染问题 

## 使用let声明变量

- ES6不仅引入let关键字用于解决变量声明的问题，同时引入了块级作用域的概念
- 块级作用域：代码执行时遇到花括号，会创建一个块级作用域，花括号结束，销毁块级作用域

### 声明变量的问题

-  全局变量挂载到全局对象：全局对象成员污染问题
   - let声明的变量不会挂载到全局对象 
-  允许重复的变量声明：导致数据被覆盖
   - let声明的变量，不允许当前作用域范围内重复声明
   - 在块级作用域中用let定义的变量，在作用域外不能访问 
-  变量提升：怪异的数据访问、闭包问题 
   - 使用let不会有变量提升，因此，不能在定义let变量之前使用它

**底层实现上，let声明的变量实际上也会有提升，但是，提升后会将其放入到“暂时性死区”，如果访问的变量位于暂时性死区，则会报错：“Cannot access 'a' before initialization”。当代码运行到该变量的声明语句时，会将其从暂时性死区中移除。**

- 在循环中，用let声明的循环变量，会特殊处理，每次进入循环体，都会开启一个新的作用域，并且将循环变量绑定到该作用域（每次循环，使用的是一个全新的循环变量）
- 在循环中使用let声明的循环变量，在循环结束后会销毁

## 使用const声明常量

- const和let完全相同，仅在于用const声明的变量，必须在声明时赋值，而且不可以重新赋值
- 实际上，在开发中，应该尽量使用const来声明变量，以保证变量的值不会随意篡改，原因如下：
  - 根据经验，开发中的很多变量，都是不会更改，也不应该更改的
  - 后续的很多框架或者是第三方JS库，都要求数据不可变，使用常量可以一定程度上保证这一点

### 注意的细节：

- 常量不可变，是指声明的常量的内存空间不可变，但并不保证内存空间中的地址指向的其他空间不可变，如对象内的数据
- 常量的命名
  - 特殊的常量：该常量从字面意义上，一定是不可变的，比如圆周率、月地距地或其他一些绝不可能变化的配置。通常，**该常量的名称全部使用大写，多个单词之间用下划线分割**
  - 普通的常量：使用和之前一样的命名即可
- 在for循环中，循环变量不可以使用常量，在for in 循环中可用，每次都是一个新的作用域

# 更好的Unicode支持

- 早期，由于存储空间宝贵，Unicode使用16位二进制来存储文字
  - 我们将一个16位的二进制编码叫做一个码元（Code Unit）
  - 后来，由于技术的发展，Unicode对文字编码进行了扩展，将某些文字扩展到了32位（占用两个码元）
  - 并且，将某个文字对应的二进制数字叫做码点（Code Point）
- ES6为了解决这个困扰，为字符串提供了方法：codePointAt，根据字符串码元的位置得到其码点
- 同时，ES6为正则表达式添加了一个`flag: u`，如果添加了该配置，则匹配时，使用码点匹配

# 更多的字符串API

## 以下均为字符串的实例（原型）方法

- includes：判断字符串中是否包含指定的子字符串
- startsWith：判断字符串中是否以指定的字符串开始
- endsWith：判断字符串中是否以指定的字符串结尾
- repeat：将字符串重复指定的次数，然后返回一个新字符串

# 正则中的粘连标记

标记名：y  粘连标志
含义：匹配时，完全按照正则对象中的 lastIndex 位置开始匹配，并且匹配的位置必须在 lastIndex 位置，lastIndex 可以改变：

```javascript
const text = "Hello World!!!";
const reg = /W\w+/y;
reg.lastIndex = 6;
console.log("reg.lastIndex:", reg.lastIndex)
console.log(reg.test(text))
```

# 模板字符串

## ES6之前处理字符串繁琐的两个方面

1. 多行字符串
2. 字符串拼接

在ES6中，提供了模板字符串的书写，可以非常方便的换行和拼接，要做的，仅仅是将字符串的开始和结尾改为```符号
如果要在字符串中拼接js表达式，只需要在模板字符串中使用`**${JS表达式}**`，模板字符串可以嵌套

## 模板字符串标记

在模板字符串书写之前，可以加上标记`标记名`模板字符串``
标记是一个函数，函数参数如下：

1. 参数1：被插值分割的字符串数组
2. 后续参数：所有的插值

```javascript
var love1 = "秋葵";
var love2 = "香菜";
var text = myTag`邓哥喜欢${love1}，邓哥也喜欢${love2}。`;
//相当于： 
// text = myTag(["邓哥喜欢", "，邓哥也喜欢", "。"], "秋葵", "香菜")
function myTag(parts) {
    const values = Array.prototype.slice.apply(arguments).slice(1);
    let str = "";
    for (let i = 0; i < values.length; i++) {
        str += `${parts[i]}：${values[i]}`;
        if (i === values.length - 1) {
            str += parts[i + 1];
        }
    }
    return str;
}
console.log(text);
```

# 函数参数默认值

## 使用

在书写形参时，直接给形参赋值，附的值即为默认值：`function sum(a, b = 1, c = 2)`
这样一来，当调用函数时，如果没有给对应的参数赋值（给它的值是 undefined），则会自动使用默认值

## 对arguments的影响

只要给函数加上参数默认值，该函数会自动变量严格模式下的规则：arguments 和形参脱离

## 留意暂时性死区

形参和ES6中的let或const声明一样，具有作用域，并且根据参数的声明顺序，存在暂时性死区

## 剩余参数

arguments的缺陷：

- 如果和形参配合使用，容易导致混乱
- 从语义上，使用arguments获取参数，由于形参缺失，无法从函数定义上理解函数的真实意图

**ES6的剩余参数专门用于收集末尾的所有参数，将其放置到一个形参数组中**

```javascript
const testFunc = (a, ...agrs) => {
  //args里收集了所有的参数
  console.log(a, agrs) // 'a', ['b', 'c']
}
testFunc('a', 'b', 'c')
```

**细节：**

- 一个函数，仅能出现一个剩余参数
- 一个函数，如果有剩余参数，剩余参数必须是最后一个参数

# 展开运算符

- 使用方式：`...要展开的东西`
- 写法和剩余参数一样，写到要调用的函数里：`sum(...agrs,3,4,5)`
- 之后还可以继续传参数

## 对数组展开 ES6

```javascript
const arr1 = [1, 2, 3, 4];
const arr2 = [0, ...arr1, 5, 6, 7, 8];
console.log(arr2) // [0, 1, 2, 3, 4, 5, 6, 7, 8];
```

进行数组的复制，不是指向同一地址

## 对对象展开 ES7

```javascript
const obj1 = {
name: 'a',
age: 12
};
const obj2 = { ...obj1 }; //  { name: 'a', age: 12 }
const obj2 = { ...obj1, name : 'b' }，// { name: 'b', age: 12 } 新的 name 会覆盖 obj1 里的 name 进行对象的复制，浅克隆，指向同一地址
```

用以下方法进行局部深度克隆

```javascript
const obj1 = {
    name: "成哥",
    age: 18,
    loves: ["邓嫂", "成嫂1", "成嫂2"],
    address: {
        country: "中国",
        province: "黑龙江",
        city: "哈尔滨"
    }
}
const obj2 = {
    ...obj1,
    name: "邓哥",
    address: {
        ...obj1.address //深克隆
    },
    loves: [...obj1.loves, "成嫂3"]  //深克隆
};
console.log(obj2)
console.log(obj1.loves === obj2.loves) // false
console.log(obj1.address === obj2.address) // false
```

# 科里化

curry 方法，科里化，用于固定某个函数前边的参数的值，得到一个新的函数，新的函数调用时，接收剩余参数即可

```javascript
function cal(a, b, c, d) {
  return a + b * c - d;
}
// curry：柯里化，用户固定某个函数的前面的参数，得到一个新的函数，新的函数调用时，接收剩余的参数
function curry(func, ...args) {
  return function(...subArgs) {
    const allArgs = [...args, ...subArgs];
    if (allArgs.length >= func.length) {
      //参数够了
      return func(...allArgs);
    } else {
      //参数不够，继续固定
      return curry(func, ...allArgs);
    }
  }
}
const newCal = curry(cal, 1, 2)
console.log(newCal(3, 4)) // 1+2*3-4
console.log(newCal(4, 5)) // 1+2*4-5
console.log(newCal(5, 6)) // 1+2*5-6
console.log(newCal(6, 7)) // 1+2*6-7
const newCal2 = newCal(8)
console.log(newCal2(9)); // 1+2*8-9
```

# new.target

ES6提供了一个特殊的API，可以使用该API在函数内部，判断该函数是否使用了new来调用
`new.target`

- 该表达式，得到的是：如果没有使用new来调用函数，则返回undefined
- 如果使用new调用函数，则得到的是new关键字后面的函数本身

# 箭头函数

回顾：this 指向

- 通过对象调用函数，this 指向对象
- 直接调用函数，this 指向全局对象
- 如果通过 new 调用函数，this 指向新创建的对象
- 如果通过 apply、call、bind 调用函数，this 指向指定的数据
- 如果是 DOM 事件函数，this 指向事件源

## 使用语法

**箭头函数是一个函数表达式，理论上，任何使用函数表达式的场景都可以使用箭头函数**

- 完整语法：`(参数1, 参数2, ...)=>{ //函数体 }`
- 如果参数只有一个，可以省略小括号: `参数 => { }`
- 如果箭头函数只有一条返回语句，可以省略大括号，和return关键字，返回对象用一对圆括号括住对象，把对象转换成表达式即可: `参数 => 返回值`

```javascript
const isOdd = num => num % 2 !== 0;
console.log(isOdd(3))
console.log(isOdd(4))
```

## 注意细节

- 箭头函数中，不存在 this、arguments、new.target，如果使用了，则使用的是函数外层的对应的this、arguments、new.target
- 箭头函数没有原型
- 箭头函数不能当作构造函数使用

## 应用场景

- 临时性使用的函数，并不会调用它，比如： 
  - 事件处理函数
  - 异步处理函数
  - 其他临时性的函数
- 为了绑定外层this的函数

# 新增的对象字面量语法

## 成员速写

如果对象字面量初始化时，成员的名称来自于一个变量，并且和变量的名称相同，则可以进行简写：`{ a: a, b: b, c: c} ---> {a, b, c}`

## 方法速写

对象字面初始化时，方法可以省略冒号和function关键字：`{ say: function(){ console.log(123) } } ---> { say(){ console.log(123) } }`

## 计算属性名

有的时候，初始化对象时，某些属性名可能来自于某个表达式的值，在 ES6，可以使用中括号来表示该属性名是通过计算得到的：

```javascript
const prop1 = "name2";
const prop2 = "age2";
const prop3 = "sayHello2";
const user = {
  [prop1]: "姬成",
  [prop2]: 100,
  [prop3](){
    console.log(this[prop1], this[prop2])
  }
}
user[prop3]();
console.log(user)
```

# Object的新增API

- Object.is：用于判断两个数据是否相等，基本上跟严格相等（===）是一致的，除了以下两点：
  - NaN 和 NaN 相等`Object.is(NaN, NaN) // 相等`
  - +0 和 -0 不相等 `Object.is(+0, -0) // 不相等`
- Object.assign：用于混合对象，`Object.assign(obj1, obj2)`，obj2会覆盖obj1，但是会改变obj1里的内容，可用一个空对象解决，`const obj = Object.assign({}, obj1, obj2)`
- Object.getOwnPropertyNames 的枚举顺序：`Object.getOwnPropertyNames` 方法之前就存在，只不过，官方没有明确要求，对属性的顺序如何排序，如何排序，完全由浏览器厂商决定
  - ES6规定了该方法返回的数组的排序方式如下：
    - 先排数字，并按照升序排序
    - 再排其他，按照书写顺序排序

- Object.setPrototypeOf：该函数用于设置某个对象的隐式原型，修改隐式原型
  - 比如：`Object.setPrototypeOf(obj1, obj2)`
  - 相当于：`obj1.__proto__ = obj2`

# 面向对象

面向对象：一种编程思想，跟具体的语言无关
对比面向过程：

- 面向过程：思考的切入点是功能的步骤
- 面向对象：思考的切入点是对象的划分

【大象装冰箱】

## 类：构造函数的语法糖

### 传统的构造函数的问题

- 属性和原型方法定义分离，降低了可读性
- 原型成员可以被枚举
- 默认情况下，构造函数仍然可以被当作普通函数使用

### 类的特点，关键字：class

- 类声明不会被提升，与 let 和 const 一样，存在暂时性死区
- 类中的所有代码均在严格模式下执行
- 类的所有方法都是不可枚举的
- 类的所有方法都无法被当作构造函数使用
- 类的构造器必须使用 new 来调用

```javascript
class Animal{
  constructor(type, name, age, sex){
    this.type = type,
      this.name = name,
      this.age = age,
      this.sex = sex
  }
  print(){
    console.log(`【种类】：${this.type}`);
    console.log(`【名字】：${this.name}`);
    console.log(`【年龄】：${this.age}`);
    console.log(`【性别】：${this.sex}`);
  }
}
const a = new Animal(`柯基`,`小小只`,`2`,`公`);
a.print();
console.log(a);
```

#### 类的的 constructor() 属性，直接指向“类”的本身

与 ES5 的行为一致，`Animal.prototype.constructor === Animal`

### 类的其他书写方式

- 可计算的成员名

```javascript
const printName = `print`;
class Animal{
  constructor(type, name, age, sex){
    this.type = type,
      this.name = name,
      this.age = age,
      this.sex = sex 
  }
  [printName](){ //用变量名作为方法名的写法
    console.log(`【种类】：${this.type}`);
    console.log(`【名字】：${this.name}`);
    console.log(`【年龄】：${this.age}`);
    console.log(`【性别】：${this.sex}`);
  }
}
const a = new Animal(`柯基`,`小小只`,`2`,`公`);

a[printName](); 
console.log(a);
```

- getter和setter
  - ES5：Object.defineProperty 可定义某个对象成员属性的读取和设置
  - 使用 getter 和 setter 控制的属性，不在原型上

```javascript
const printName = `print`;
class Animal {
  constructor(type, name, age, sex) {
    this.type = type,
      this.name = name,
      this.age = age,
      this.sex = sex
  }
  //创建一个age属性，并给它加上getter，读取该属性时，会运行该函数
  get age() {
    return this._age + '岁';
  }
  //创建一个age属性，并给它加上setter，给该属性赋值时，会运行该函数
  set age(age) {
    if (typeof (age) !== 'number') {
      throw new TypeError('age property must be a number');
    } else if (age < 0) {
      age = 0;
    } else if (age > 1000) {
      age = 1000;
    }
    this._age = age;
  }
  [printName]() { //用变量名作为方法名的写法z
    console.log(`【种类】：${this.type}`);
    console.log(`【名字】：${this.name}`);
    console.log(`【年龄】：${this.age}`);
    console.log(`【性别】：${this.sex}`);
  }
}
const a = new Animal(`柯基`, `小小只`, 1234, `公`);
a[printName]();
console.log(a);
```

- 静态成员
  - 构造函数本身的成员
  - 使用static关键字定义的成员即静态成员

```javascript
class Chess{
  constructor(name){
    this.name = name;
  }
  static width = 50;
  static height = 50;  //static 关键字添加静态成员
  static method(){
    console.log(this.width,this.height);
  }
}
console.log(Chess.width,Chess.height);
Chess.method();
```

- 字段初始化器（ES7）

注意：

- 使用static的字段初始化器，添加的是静态成员
- 没有使用static的字段初始化器，添加的成员位于对象上
- 箭头函数在字段初始化器位置上，指向当前对象

```javascript
class Text{
  static a = 1; //静态成员
  b = 2; // 字段初始化器
  c = 3; //本身固定值的实例成员不用写在constructor构造器里
  constructor(){
    this.d = this.b + this.c;
  }
}
const a = new Text();
console.log(a);
```

- 类表达式

```javascript
const A = class { //匿名类，类表达式
  static a = 1; //静态成员
  b = 2;
  c = 3; //本身固定值的实例成员不用写在constructor里
  constructor(){
    this.d = this.b + this.c;
  }
}
```

- 装饰器（ES7）(Decorator)
  - 横切关注点
  - 装饰器的本质是一个函数

```javascript
class Test {
  @Obsolete
  print() {
    console.log("print方法")
  }
}
function Obsolete(target, methodName, descriptor) {
  // function Test
  // print
  // { value: function print(){}, ... }
  // console.log(target, methodName, descriptor);
  const oldFunc = descriptor.value
  descriptor.value = function (...args) {
    console.warn(`${methodName}方法已过时`);
    oldFunc.apply(this, args);
  }
}
```

### 类的继承

- 如果两个类A和B，如果可以描述为：B 是 A，则，A和B形成继承关系，比如猫是动物，A代表一个大类，B代表一个小支
- 如果B是A，则：
  - B继承自A
  - A派生B
  - B是A的子类
  - A是B的父类
- 如果A是B的父类，则B会自动拥有A中的所有实例成员。
- 新的关键字：
  - extends：继承，用于类的定义
  - super 
    - 直接当作函数调用，表示父类构造函数
    - 如果当作对象使用，则表示父类的原型

```javascript
class Animal {
    constructor(type, name, age, sex) {
        if (new.target === Animal) {
            throw new TypeError("你不能直接创建Animal的对象，应该通过子类创建")
        }
        this.type = type;
        this.name = name;
        this.age = age;
        this.sex = sex;
    }
    print() {
        console.log(`【种类】：${this.type}`);
        console.log(`【名字】：${this.name}`);
        console.log(`【年龄】：${this.age}`);
        console.log(`【性别】：${this.sex}`);
    }
    jiao() {
        throw new Error("动物怎么叫的？");
    }
}
class Dog extends Animal {
    constructor(name, age, sex) {
        super("犬类", name, age, sex);
        // 子类特有的属性
        this.loves = "吃骨头";
    }
    print() {
        //调用父类的print
        super.print();
        //自己特有的代码
        console.log(`【爱好】：${this.loves}`);
    }

    //同名方法，会覆盖父类
    jiao() {
        console.log("旺旺！");
    }
}
const a = new Dog("旺财", 3, "公")
a.print();
```

**注意：**

- ES6要求，如果定义了 constructor，并且该类是子类，则必须在 constructo r的第一行手动调用父类的构造函数`super()`
- 如果子类不写 constructor，则会有默认的构造器，该构造器需要的参数和父类一致，并且自动调用父类构造器

**冷知识**

- 用 JS 制作抽象类 
  - 抽象类：一般是父类，不能通过该类创建对象
- 正常情况下，this 始终指向具体的类的对象

# 解构

## 对象解构

### 什么是解构

- 使用ES6的一种语法规则，将一个对象或数组的某个属性提取到某个变量中
- **解构不会对被解构的目标造成任何影响**

```javascript
const user = {
    name: "kevin",
    age: 11,
    sex: "男",
    address: {
        province: "四川",
        city: "成都"
    }
}
// let name, age, sex, address;
// name = user.name;
// age = user.age;
// sex = user.sex;
// address = user.address;
// let name, age, sex, address, abc;
// ({ name, age, sex, address } = user);
// 先定义5个变量，然后从对象中读取同名属性，放到变量中
let { name, age, sex, address, abc = 123 } = user
console.log(name, age, sex, address, abc)
```

### 在解构中使用默认值

**{同名变量 = 默认值}**

```javascript
let { name, age, sex, address, abc = 123 } = user
// abc在对象中有值就用对象中的值，没有值用默认值123
```

### 非同名属性解构

{属性名:变量名}

```javascript
// gender 没有同名属性，读取 sex 的属性, sex没值用默认值 性别, 在这个里 gender 即取的对象中的 sex 的值
let { name, age, sex: gender = "性别", address, abc = 123 } = user
console.log(name, age, gender, address, abc)
```

### 深层次解构

```javascript
const user = {
    name: "kevin",
    age: 11,
    sex: "男",
    address: {
        province: "四川",
        city: "成都"
    }
}
// 解构出 user 中的 name、address.province
// 定义两个变量 name、province
// 再解构
const { name, address: { province } } = user;
console.log(name, province)
```

## 数组解构

与对象可以一模一样，也可以更简单：

```javascript
const number = ['a', 'b', [1, 2, 3, 4], 'd', {
    q: 'x',
    w: 'y',
    e: 'z'
}];
// let [n1, n2, n3] = number;
// console.log(n1, n2, n3);
// let [n1, , , n4, n5 = 123] = number;
// console.log(n1, n4, n5);
// let [n1, , [a, b, , d], n4, n5 = 123] = number;
// console.log(n1, a, b, d, n4, n5);
// let [n1, , [a, b, , d], n4, {
//     q,
//     w: R,
//     e
// }] = number;
// console.log(n1, a, b, d, n4, q, R, e);
let [n1, n2, ...obj] = number;
console.log(n1, n2, obj);
let a = 1, b = 2;
[b, a] = [a, b];
console.log(a,b);
```

## 参数结构

```javascript
 // function print(user) {
//     console.log(`姓名：${user.name}`)
//     console.log(`年龄：${user.age}`)
//     console.log(`性别：${user.sex}`)
//     console.log(`身份：${user.address.province}`)
//     console.log(`城市：${user.address.city}`)
// }
function print({ name, age, sex, address: {
    province,
    city
} }) {  //直接把传入的参数对象解构
    console.log(`姓名：${name}`)
    console.log(`年龄：${age}`)
    console.log(`性别：${sex}`)
    console.log(`身份：${province}`)
    console.log(`城市：${city}`)
}
const user = {
    name: "kevin",
    age: 11,
    sex: "男",
    address: {
        province: "四川",
        city: "成都"
    }
}
print(user)
// function ajax(options) {
//     const defaultOptions = {
//         method: "get",
//         url: "/"
//     }
//     const opt = {
//         ...defaultOptions,
//         ...options
//     }
//     console.log(opt)
// }
function ajax({
    method = "get",
    url = "/"
} = {}) { // 解构参数对象，如果没有传参，则使用默认值{}，不传参解构会报错，无法解构undefined和null
    console.log(method, url)
}
ajax()
```

# 符号 Symbol()

## 普通符号

- 符号是ES6新增的一个数据类型，它通过使用函数 `Symbol(符号描述)` 来创建`let sym1 = Symbol('123');`
- 符号设计的初衷，是为了给对象设置私有属性
  - 私有属性：只能在对象内部使用，外面无法使用

```javascript
//创建一个符号
const syb1 = Symbol();
const syb2 = Symbol("abc");
console.log(syb1, syb2);
console.log(typeof syb1 === "symbol", typeof syb2 === "symbol")
```

符号具有以下特点：

- 没有字面量
- 使用 typeof 得到的类型是 symbol
- **每次调用 Symbol 函数得到的符号永远不相等，无论符号名是否相同**
- 符号可以作为对象的属性名存在，这种属性称之为符号属性`[sym1]: 3`，对象中符号属性名需用 [ ] 括住 
  - 开发者可以通过精心的设计，让这些属性无法通过常规方式被外界访问
  - 符号属性是不能枚举的，因此在 for-in 循环中无法读取到符号属性，Object.keys 方法也无法读取到符号属性
  - Object.getOwnPropertyNames 尽管可以得到所有无法枚举的属性，但是仍然无法读取到符号属性
  - ES6 新增 Object.getOwnPropertySymbols 方法，可以读取符号
- 符号无法被隐式转换，因此不能被用于数学运算、字符串拼接或其他隐式转换的场景，但符号可以显式的转换为字符串，通过 String 构造函数进行转换即可，console.log 之所以可以输出符号，是它在内部进行了显式转换

```javascript
const Hero = (() => {
  const getRandom = Symbol();

  return class {
    constructor(attack, hp, defence) {
      this.attack = attack;
      this.hp = hp;
      this.defence = defence;
    }

    gongji() {
      //伤害：攻击力*随机数（0.8~1.1)
      const dmg = this.attack * this[getRandom](0.8, 1.1);
      console.log(dmg);
    }

    [getRandom](min, max) { //根据最小值和最大值产生一个随机数
      return Math.random() * (max - min) + min;
    }
  }
})();
const h = new Hero(3, 6, 3);
console.log(h);
const syb = Symbol();
const obj = {
  [syb]: 1,
  a: 2,
  b: 3
}
for (const prop in obj) {
  console.log(prop)
}
console.log(Object.keys(obj)) //Object.keys 返回一个所有元素为字符串的数组，其元素来自于从给定的object上面可直接枚举的属性。这些属性的顺序与手动遍历该对象属性时的一致。
console.log(Object.getOwnPropertyNames(obj)) //Object.getOwnPropertyNames()本身不包含对象的 Symbol 属性，只包含字符串属性。返回一个数组，该数组对元素是 obj自身拥有的枚举或不可枚举属性名称字符串。 数组中枚举属性的顺序与通过 for...in 循环（或 Object.keys）迭代该对象属性时一致。数组中不可枚举属性的顺序未定义。
//得到的是一个符号属性的数组
const sybs = Object.getOwnPropertySymbols(obj); //返回 Symbol 属性的对象,在给定对象自身上找到的所有 Symbol 属性的数组。
console.log(sybs, sybs[0] === syb)
```

## 共享符号

根据某个符号名称（符号描述）能够得到同一个符号

```javascript
Symbol.for("符号名/符号描述")  //获取共享符号，静态成员
const obj1 = Symbol.for('abc');
const obj2 = Symbol.for('abc');
obj1 === obj2;
```

## 知名（公共、具名）符号

知名符号是一些具有特殊含义的共享符号，天生就有，不用创建，直接用，通过 Symbol 的静态属性得到
ES6 延续了 ES5 的思想：减少魔法，暴露内部实现！
因此，ES6 用知名符号暴露了某些场景的内部实现

- Symbol.hasInstance：该符号用于定义构造函数的静态成员，它将影响 instanceof 的判定

```javascript
obj instanceof A
//等效于
A[Symbol.hasInstance](obj) // Function.prototype[Symbol.hasInstance]
```

- Symbol.isConcatSpreadable：该知名符号会影响数组的 concat 方法
- Symbol.toPrimitive：该知名符号会影响类型转换的结果
- Symbol.toStringTag：该知名符号会影响 Object.prototype.toString 的返回值
- 其他知名符号

# 事件循环

- JS运行的环境称之为宿主环境
- 执行栈：call stack，一个数据结构，用于存放各种函数的执行环境，每一个函数执行之前，它的相关信息会加入到执行栈。函数调用之前，创建执行环境，然后加入到执行栈；函数调用之后，销毁执行环境
- JS引擎永远执行的是执行栈的最顶部
- 异步函数：某些函数不会立即执行，需要等到某个时机到达后才会执行，这样的函数称之为异步函数。比如事件处理函数。异步函数的执行时机，会被宿主环境控制
- 浏览器宿主环境中包含5个线程：
  - JS引擎：负责执行执行栈的最顶部代码
  - GUI线程：负责渲染页面
  - 事件监听线程：负责监听各种事件
  - 计时线程：负责计时
  - 网络线程：负责网络通信
- 当上面的线程发生了某些事请，如果该线程发现，这件事情有处理程序，它会将该处理程序加入一个叫做事件队列的内存。当JS引擎发现，执行栈中已经没有了任何内容后，会将事件队列中的第一个函数加入到执行栈中执行
- JS引擎对事件队列的取出执行方式，以及与宿主环境的配合，称之为事件循环。
- 事件队列在不同的宿主环境中有所差异，大部分宿主环境会将事件队列进行细分。在浏览器中，事件队列分为两种：
  - 宏任务（队列）：macroTask，计时器结束的回调、事件回调、http回调等等绝大部分异步函数进入宏队列
  - 微任务（队列）：MutationObserver，Promise产生的回调进入微队列
    - MutationObserver用于监听某个DOM对象的变化
- 当执行栈清空时，JS引擎首先会将微任务中的所有任务依次执行结束，如果没有微任务，则执行宏任务

## 事件和回调函数的缺陷

- 我们习惯于使用传统的回调或事件处理来解决异步问题
  - 事件：某个对象的属性是一个函数，当发生某一件事时，运行该函数
    - `dom.onclick = function() {}`
  - 回调：运行某个函数以实现某个功能的时候，传入一个函数作为参数，当发生某件事的时候，会运行该函数
    - dom.addEventListener("click", function(){})
- 本质上，事件和回调并没有本质的区别，只是把函数放置的位置不同而已。
- 一直以来，该模式都运作良好
- 直到前端工程越来越复杂...
- 目前，该模式主要面临以下两个问题：
  - 回调地狱：某个异步操作需要等待之前的异步操作完成，无论用回调还是事件，都会陷入不断的嵌套
  - 异步之间的联系：某个异步操作要等待多个异步操作的结果，对这种联系的处理，会让代码的复杂度剧增

## 异步处理的通用模型

- ES官方参考了大量的异步场景，总结出了一套异步的通用模型，该模型可以覆盖几乎所有的异步场景，甚至是同步场景。
- 值得注意的是，为了兼容旧系统，ES6 并不打算抛弃掉过去的做法，只是基于该模型推出一个全新的 API，使用该API，会让异步处理更加的简洁优雅。
- 理解该 API，最重要的，是理解它的异步模型
  - ES6 将某一件可能发生异步操作的事情，分为两个阶段：**unsettled** 和 **settled**
    - unsettled： 未决阶段，表示事情还在进行前期的处理，并没有发生通向结果的那件事
    - settled：已决阶段，事情已经有了一个结果，不管这个结果是好是坏，整件事情无法逆转

<!-- ![image.png](https://cdn.nlark.com/yuque/0/2022/png/2675710/1644480687145-4f811ab3-9414-4c27-a7f9-5ec6b916bb0a.png#averageHue=%23c7d5ed&clientId=u0a22fc2b-3616-4&from=paste&height=297&id=u67ab9809&name=image.png&originHeight=297&originWidth=956&originalType=binary&ratio=1&rotation=0&showTitle=false&size=17550&status=done&style=none&taskId=ud5a592a8-8f3e-4169-bf3b-b9560c4a4da&title=&width=956) -->

      - 事情总是从 未决阶段 逐步发展到 已决阶段的。并且，未决阶段拥有控制何时通向已决阶段的能力

   - ES6将事情划分为三种状态： pending、resolved、rejected
     - pending: 挂起，处于未决阶段，则表示这件事情还在挂起（最终的结果还没出来）
     - resolved：已处理，已决阶段的一种状态，表示整件事情已经出现结果，并是一个可以按照正常逻辑进行下去的结果
     - rejected：已拒绝，已决阶段的一种状态，表示整件事情已经出现结果，并是一个无法按照正常逻辑进行下去的结果，通常用于表示有一个错误
   - 既然未决阶段有权力决定事情的走向，因此，未决阶段可以决定事情最终的状态！
     - 我们将 把事情变为 resolved 状态的过程叫做：**resolve**，推向该状态时，可能会传递一些数据
     - 我们将 把事情变为 rejected 状态的过程叫做：**reject**，推向该状态时，同样可能会传递一些数据，通常为错误信息
   - **始终记住，无论是阶段，还是状态，都是不可逆的！**

<!-- ![image.png](https://cdn.nlark.com/yuque/0/2022/png/2675710/1644480930734-17fb4592-9cd4-4828-9f94-d3d13abdd343.png#averageHue=%23ed8037&clientId=u0a22fc2b-3616-4&from=paste&height=617&id=uf07107c9&name=image.png&originHeight=617&originWidth=1238&originalType=binary&ratio=1&rotation=0&showTitle=false&size=79623&status=done&style=none&taskId=ud3b326df-08af-4405-b759-e4cb9f53eb2&title=&width=1238) -->

   - 当事情达到已决阶段后，通常需要进行后续处理，不同的已决状态，决定了不同的后续处理
     - resolved状态：这是一个正常的已决状态，后续处理表示为 thenable
     - rejected状态：这是一个非正常的已决状态，后续处理表示为 catchable
   - 后续处理可能有多个，因此会形成作业队列，这些后续处理会按照顺序，当状态到达后依次执行

<!-- ![image.png](https://cdn.nlark.com/yuque/0/2022/png/2675710/1644481075275-70215511-94e8-4990-a696-605683fcc823.png#averageHue=%23e69d63&clientId=u0a22fc2b-3616-4&from=paste&height=647&id=uef9493e7&name=image.png&originHeight=647&originWidth=1237&originalType=binary&ratio=1&rotation=0&showTitle=false&size=98202&status=done&style=none&taskId=udc0f03d3-4ce0-4c3c-9f8e-ff0b2d064b3&title=&width=1237) -->

   - 整件事称之为Promise

## Promise的基本使用

```javascript
const pro = new Promise((resolve, reject)=>{
  // 未决阶段的处理
  // 通过调用resolve函数将Promise推向已决阶段的resolved状态
  // 通过调用reject函数将Promise推向已决阶段的rejected状态
  // resolve和reject均可以传递最多一个参数，表示推向状态的数据
})
pro.then(data=>{
  //这是thenable函数，如果当前的Promise已经是resolved状态，该函数会立即执行
  //如果当前是未决阶段，则会加入到作业队列，等待到达resolved状态后执行
  //data为状态数据
}, err=>{
  //这是catchable函数，如果当前的Promise已经是rejected状态，该函数会立即执行
  //如果当前是未决阶段，则会加入到作业队列，等待到达rejected状态后执行
  //err为状态数据
})
// 辅助函数,把传进来的对象拼接成url的字符串
function toData(obj) {
  if (obj === null) {
    return obj;
  }
  let arr = [];
  for (let i in obj) {
    let str = i + "=" + obj[i];
    arr.push(str);
  }
  return arr.join("&");
}
// 封装Ajax
function ajax(obj) {
  return new Promise((resolve, reject) => {
    //指定提交方式的默认值
    obj.type = obj.type || "get";
    //设置是否异步，默认为true(异步)
    obj.async = obj.async || true;
    //设置数据的默认值
    obj.data = obj.data || null;
    // 根据不同的浏览器创建XHR对象
    let xhr = null;
    if (window.XMLHttpRequest) {
      // 非IE浏览器
      xhr = new XMLHttpRequest();
    } else {
      // IE浏览器
      xhr = new ActiveXObject("Microsoft.XMLHTTP");
    }
    // 区分get和post,发送HTTP请求
    if (obj.type === "post") {
      xhr.open(obj.type, obj.url, obj.async);
      xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
      let data = toData(obj.data);
      xhr.send(data);
    } else {
      let url = obj.url + "?" + toData(obj.data);
      xhr.open(obj.type, url, obj.async);
      xhr.send();
    }
    // 接收返回过来的数据
    xhr.onreadystatechange = function() {
      if (xhr.readyState === 4) {
        if (xhr.status >= 200 && xhr.status < 300 || xhr.status == 304) {
          resolve(JSON.parse(xhr.responseText))
        } else {
          reject(xhr.status)
        }
      }
    }
  })
}  
ajax({
  url: "./data/students.json?name=李华"
}).then(resp => {
  console.log(resp)
}, err => {
  console.log(err)
})
```

**细节**

- 未决阶段的处理函数是同步的，会立即执行
- thenable 和 catchable 函数是异步的，就算是立即执行，也会加入到事件队列中等待执行，并且，加入的队列是微队列
- pro.then 可以只添加 thenable 函数，pro.catch 可以单独添加 catchable 函数
- 在未决阶段的处理函数中，如果发生未捕获的错误，会将状态推向 rejected，并会被 catchable 捕获
- 一旦状态推向了已决阶段，无法再对状态做任何更改
- **Promise 并没有消除回调，只是让回调变得可控**

### Promise的串联

- 当后续的 Promise 需要用到之前的 Promise 的处理结果时，需要 Promise 的串联
- Promise 对象中，无论是 then 方法还是 catch 方法，它们都具有返回值，返回的是一个全新的 Promise 对象，它的状态满足下面的规则：
  - 如果当前的 Promise 是未决的，得到的新的 Promise 是挂起状态
  - 如果当前的 Promise 是已决的，会运行响应的后续处理函数，并将后续处理函数的结果（返回值）作为 resolved 状态数据，应用到新的 Promise 中；如果后续处理函数发生错误，则把返回值作为 rejected 状态数据，应用到新的 Promise 中
- **后续的 Promise 一定会等到前面的 Promise 有了后续处理结果后，才会变成已决状态**
- 如果前面的 Promise 的后续处理，返回的是一个 Promise，则返回的新的 Promise 状态和后续处理返回的 Promise 状态保持一致

```javascript
//获取李华所在班级的老师的信息
//1. 获取李华的班级id   Promise
//2. 根据班级id获取李华所在班级的老师id   Promise
//3. 根据老师的id查询老师信息   Promise
const pro = ajax({
  url: "./data/students.json"
})
pro.then(resp => {
  for (let i = 0; i < resp.length; i++) {
    if (resp[i].name === "李华") {
      return resp[i].classId; //班级id
    }
  }
}).then(cid => {
  return ajax({
    url: "./data/classes.json?cid=" + cid
  }).then(cls => {
    for (let i = 0; i < cls.length; i++) {
      if (cls[i].id === cid) {
        return cls[i].teacherId;
      }
    }
  })
}).then(tid => {
  return ajax({
    url: "./data/teachers.json"
  }).then(ts => {
    for (let i = 0; i < ts.length; i++) {
      if (ts[i].id === tid) {
        return ts[i];
      }
    }
  })
}).then(teacher => {
  console.log(teacher);
})
function biaobai(god) {
  return new Promise(resolve => {
    console.log(`邓哥向${god}发出了表白短信`);
    setTimeout(() => {
      if (Math.random() < 0.3) {
        //女神同意拉
        resolve(true)
      } else {
        //resolve
        resolve(false);
      }
    }, 500);
  })
}
/*
    邓哥心中有三个女神
    有一天，邓哥决定向第一个女神表白，如果女神拒绝，则向第二个女神表白，直到所有的女神都拒绝，或有一个女神同意为止
    用代码模拟上面的场景
*/
const gods = ["女神1", "女神2", "女神3", "女神4", "女神5"];
let pro;
for (let i = 0; i < gods.length; i++) {
  if (i === 0) {
    pro = biaobai(gods[i]);
  }
  pro = pro.then(resp => {
    if (resp === undefined) {
      return;
    } else if (resp) {
      console.log(`${gods[i]}同意了`)
      return;
    } else {
      console.log(`${gods[i]}拒绝了`)
      if (i < gods.length - 1) {
        return biaobai(gods[i + 1]);
      }
    }
  })
}
// let pro = biaobai(gods[0]).then(resp => {
//     if (resp === undefined) {
//         return;
//     } else if (resp) {
//         console.log(`${gods[0]}同意了`)
//         return;
//     } else {
//         console.log(`${gods[0]}拒绝了`)
//         return biaobai(gods[1]);
//     }
// });
// pro = pro.then(resp => {
//     if (resp === undefined) {
//         return;
//     } else if (resp) {
//         console.log(`${gods[1]}同意了`)
//         return;
//     } else {
//         console.log(`${gods[1]}拒绝了`)
//         return biaobai(gods[2]);
//     }
// })
// pro = pro.then(resp => {
//     if (resp === undefined) {
//         return;
//     } else if (resp) {
//         console.log(`${gods[2]}同意了`)
//         return;
//     } else {
//         console.log(`${gods[2]}拒绝了`)
//     }
// })
// biaobai("女神1").then(resp => {
//     if (resp) {
//         console.log("女神1同意了")
//         return;
//     } else {
//         return biaobai("女神2");
//     }
// }).then(resp => {
//     if (resp === undefined) {
//         return;
//     } else if (resp) {
//         console.log("女神2同意了")
//         return;
//     } else {
//         return biaobai("女神3");
//     }
// }).then(resp => {
//     if (resp === undefined) {
//         return;
//     } else if (resp) {
//         console.log("女神3同意了")
//     } else {
//         console.log("都被拒绝了！");
//     }
// })
```

### Promise的其他api

#### 原型成员 (实例成员)

- then：注册一个后续处理函数，当Promise为resolved状态时运行该函数
- catch：注册一个后续处理函数，当Promise为rejected状态时运行该函数
- finally：[ES2018]注册一个后续处理函数（无参），当Promise为已决时运行该函数

#### 构造函数成员 （静态成员）

-  resolve(数据)：该方法返回一个resolved状态的Promise，传递的数据作为状态数据 
   - 特殊情况：如果传递的数据是Promise，则直接返回传递的Promise对象
-  reject(数据)：该方法返回一个rejected状态的Promise，传递的数据作为状态数据 
-  all(iterable)：这个方法返回一个新的promise对象，该promise对象在iterable参数对象里所有的promise对象都成功的时候才会触发成功，一旦有任何一个iterable里面的promise对象失败则立即触发该promise对象的失败。这个新的promise对象在触发成功状态以后，会把一个包含iterable里所有promise返回值的数组作为成功回调的返回值，顺序跟iterable的顺序保持一致；如果这个新的promise对象触发了失败状态，它会把iterable里第一个触发失败的promise对象的错误信息作为它的失败错误信息。Promise.all方法常被用于处理多个promise对象的状态集合。 
-  race(iterable)：当iterable参数里的任意一个子promise被成功或失败后，父promise马上也会用子promise的成功返回值或失败详情作为参数调用父promise绑定的相应句柄，并返回该promise对象 

#### async 和 await

async 和 await 是 ES2016 新增两个关键字，它们借鉴了 ES2015 中生成器在实际开发中的应用，目的是简化 Promise api 的使用，并非是替代 Promise。

- async
  - 目的是简化在函数的返回值中对Promise的创建
  - async 用于修饰函数（无论是函数字面量还是函数表达式），放置在函数最开始的位置，被修饰函数的返回结果一定是 Promise 对象。

```javascript
async function test(){
  console.log(1);
  return 2;
}
//等效于
function test(){
  return new Promise((resolve, reject)=>{
    console.log(1);
    resolve(2);
  })
}
```

- await
  - **await 关键字必须出现在 async 函数中！！！**
  - await 用在某个表达式之前，如果表达式是一个Promise，则得到的是 thenable 中的状态数据

```javascript
async function test1(){
  console.log(1);
  return 2;
}
async function test2(){
  const result = await test1();
  console.log(result);
}
test2();
```

等效于

```javascript
function test1(){
  return new Promise((resolve, reject)=>{
    console.log(1);
    resolve(2);
  })
}
function test2(){
  return new Promise((resolve, reject)=>{
    test1().then(data => {
      const result = data;
      console.log(result);
      resolve();
    })
  })
}
test2();
```

如果await的表达式不是Promise，则会将其使用Promise.resolve包装后按照规则运行

## Promise的理解

- Promise是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大
- 它由社区最早提出和实现，ES6将其写进了语言标准，统一了用法，原生提供了Promise对象
- 所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果
- 从语法上说，Promise是一个对象，从它可以获取异步操作的消息
- Promise提供统一的API，各种异步操作都可以用同样的方法进行处理
- 有了Promise对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数
- 此外，Promise对象提供统一的接口，使得控制异步操作更加容易

### Promise缺点

- 无法取消Promise，一旦新建它就会立即执行，无法中途取消
- 如果不设置回调函数，Promise内部抛出的错误，不会反应到外部
- 当处于Pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）
- 同步调用，在发起一个函数或方法调用时，没有得到结果之前，该调用就不返回，直到返回结果
  - 异步调用的概念和同步相对
    - 在一个异步调用发起后，被调用者立即返回给调用者，但调用者不能立刻得到结果
    - 被调用者在实际处理这个调用的请求完成后，通过状态、通知或回调等方式来通知调用者请求处理的结果
  - 简单地说，同步就是发出一个请求后什么事都不做，一直等待请求返回后才会继续做事
  - 异步就是发出请求后继续去做其他事，这个请求处理完成后会通知你，这时候就可以处理这个回应了

## async/await的理解

- async/await其实是Promise的语法糖，它能实现的效果都能用then链来实现
  - 它是为优化then链而开发出来的
  - 从字面上来看，async是“异步”的简写
  - await译为等待
  - 所以我们很好理解async声明function是异步的，await等待某个操作完成
- await等待的是一个Promise对象，或者是其他值（也就是说可以等待任何值）
  - 如果等待的是Promise对象，则返回Promise的处理结果
  - 如果是其他值，则返回该值本身
  - 并且await会暂停当前async function的执行，等待Promise的处理完成
    - 若Promise正常处理（fulfillded），其将回调的resolve函数参数作为await表达式的值，继续执行async function
    - 若Promise处理异常（rejected），await表达式会把Promise异常原因抛出
    - 另外如果await操作符后面的表达式不是一个Promise对象，则返回该值本身

# Fetch Api

## XMLHttpRequest的问题

- 所有的功能全部集中在同一个对象上，容易书写出混乱不易维护的代码
- 采用传统的事件驱动模式，无法适配新的 Promise Api

## Fetch Api 的特点

- 并非取代 AJAX，而是对 AJAX 传统 API 的改进
- 精细的功能分割：头部信息、请求信息、响应信息等均分布到不同的对象，更利于处理各种复杂的 AJAX 场景
- 使用 Promise Api，更利于异步代码的书写
- Fetch Api 并非 ES6 的内容，属于 HTML5 新增的 Web Api
- 需要掌握网络通信的知识

```javascript
const upload = async () => {
  const inp = document.querySelector('#avatar');
  if(inp.files.length === 0) {
    alert('请选择需要上传的文件');
    return;
  }

  const formData = new FormData();
  formData.append('imagefile', inp.files[0]);
  const url = "http://101.132.72.36:5100/api/upload";
  const resp = await fetch(url, {
    method: "POST",
    body: formData
  });
  const result = await resp.json();
  return result;
}
document.querySelector('button').onclick = async () => {
  const result = await upload();
  const img = document.querySelector('#imgAvatar');
  img.src = result.path;
}
```

## 基本使用

> 请求测试地址：[http://101.132.72.36:5100/api/local](http://101.132.72.36:5100/api/local)

使用 `fetch` 函数即可立即向服务器发送网络请求

### 参数

该函数有两个参数：

1. 必填，字符串，请求地址
2. 选填，对象，请求配置
   - method：字符串，请求方法，默认值GET
   - headers：对象，请求头信息
   - body: 请求体的内容，必须匹配请求头中的 Content-Type
   - mode：字符串，请求模式 
     - cors：默认值，配置为该值，会在请求头中加入 origin 和 referer
     - no-cors：配置为该值，不会在请求头中加入 origin 和 referer，跨域的时候可能会出现问题
     - same-origin：指示请求必须在同一个域中发生，如果请求其他域，则会报错
   - credentials: 如何携带凭据（cookie） 
     - omit：默认值，不携带cookie
     - same-origin：请求同源地址时携带cookie
     - include：请求任何地址都携带cookie
   - cache：配置缓存模式 
     - default: 表示fetch请求之前将检查下http的缓存.
     - no-store: 表示fetch请求将完全忽略http缓存的存在. 这意味着请求之前将不再检查下http的缓存, 拿到响应后, 它也不会更新http缓存.
     - no-cache: 如果存在缓存, 那么fetch将发送一个条件查询request和一个正常的request, 拿到响应后, 它会更新http缓存.
     - reload: 表示fetch请求之前将忽略http缓存的存在, 但是请求拿到响应后, 它将主动更新http缓存.
     - force-cache: 表示fetch请求不顾一切的依赖缓存, 即使缓存过期了, 它依然从缓存中读取. 除非没有任何缓存, 那么它将发送一个正常的request.
     - only-if-cached: 表示fetch请求不顾一切的依赖缓存, 即使缓存过期了, 它依然从缓存中读取. 如果没有缓存, 它将抛出网络错误(该设置只在mode为”same-origin”时有效).

### 返回值

fetch 函数返回一个 Promise 对象

- 当收到服务器的返回结果后，Promise 进入resolved状态，状态数据为 Response 对象
- 当网络发生错误（或其他导致无法完成交互的错误）时，Promise 进入 rejected 状态，状态数据为错误信息

#### Response对象

- ok：boolean，当响应消息码在200~299之间时为true，其他为false
- status：number，响应的状态码
- text()：用于处理文本格式的 Ajax 响应。它从响应中获取文本流，将其读完，然后返回一个被解决为 string 对象的 Promise。
- blob()：用于处理二进制文件格式（比如图片或者电子表格）的 Ajax 响应。它读取文件的原始数据，一旦读取完整个文件，就返回一个被解决为 blob 对象的 Promise。
- json()：用于处理 JSON 格式的 Ajax 的响应。它将 JSON 数据流转换为一个被解决为 JavaScript 对象的promise。
- redirect()：可以用于重定向到另一个 URL。它会创建一个新的 Promise，以解决来自重定向的 URL 的响应。

### Request 对象

- 除了使用基本的fetch方法，还可以通过创建一个Request对象来完成请求（实际上，fetch的内部会帮你创建一个Request对象）`new Request(url地址, 配置)`
- **尽量保证每次请求都是一个新的Request对象**

### Headers 对象

- 在Request和Response对象内部，会将传递的请求头对象，转换为Headers
- Headers对象中的方法：
  - has(key)：检查请求头中是否存在指定的key值
  - get(key): 得到请求头中对应的key值
  - set(key, value)：修改对应的键值对
  - append(key, value)：添加对应的键值对
  - keys(): 得到所有的请求头键的集合
  - values(): 得到所有的请求头中的值的集合
  - entries(): 得到所有请求头中的键值对的集合

## 文件上传

流程：

1. 客户端将文件数据发送给服务器
2. 服务器保存上传的文件数据到服务器端
3. 服务器响应给客户端一个文件访问地址

> 测试地址：[http://101.132.72.36:5100/api/upload](http://101.132.72.36:5100/api/upload)
> 键的名称（表单域名称）：imagefile

- 请求方法：POST
- 请求的表单格式：（常用）multipart/form-data   没有严格规定
- 请求体中必须包含一个键值对，键的名称是服务器要求的名称，值是文件数据

> HTML5中，JS仍然无法随意的获取文件数据，但是可以获取到input元素中，被用户选中的文件数据
> 可以利用HTML5提供的FormData构造函数来创建请求体
> 表单字段名需要和服务器进行约定

# 迭代器

## 背景知识

- 什么是迭代？
  - 从一个数据集合中按照一定的顺序，不断取出数据的过程
- 迭代和遍历的区别？
  - 迭代强调的是依次取数据，并不保证取多少，也不保证把所有的数据取完
  - 遍历强调的是要把整个数据依次全部取出
- 迭代器
  - 对迭代过程的封装，在不同的语言中有不同的表现形式，通常为对象
- 迭代模式
  - 一种设计模式，用于统一迭代过程，并规范了迭代器规格：
    - 迭代器应该具有得到下一个数据的能力
    - 迭代器应该具有判断是否还有后续数据的能力

## JS中的迭代器

- JS规定，如果一个对象具有next方法，并且该方法返回一个对象，该对象的格式如下：
  - `{value: 值, done: 是否迭代完成}`
- 则认为该对象是一个迭代器

含义：

- next方法：用于得到下一个数据
- 返回的对象 
  - value：下一个数据的值
  - done：boolean，是否迭代完成

## 可迭代协议 与 for-of 循环

### 可迭代协议

#### 概念回顾

- 迭代器(iterator)：一个具有next方法的对象，next方法返回下一个数据并且能指示是否迭代完成
- 迭代器创建函数（iterator creator）：一个返回迭代器的函数

#### 可迭代协议

ES6规定，如果一个对象具有知名符号属性`Symbol.iterator`，并且属性值是一个迭代器创建函数，则该对象是可迭代的（iterable）

```javascript
let divs = document.querySelectorAll('div');
const died = divs[Symbol.iterator]();
let result = died.next();
while(!result.done){
    console.log(result.value);
    result = died.next();
}
```

### for-of 循环

for-of 循环用于遍历可迭代对象，格式如下

```javascript
//迭代完成后循环结束
for(const item in iterable){
    //iterable：可迭代对象
    //item：每次迭代得到的数据
}
for(const item of divs){
    console.log(item);
}
```

## 展开运算符与可迭代对象

展开运算符可以作用于可迭代对象，这样，就可以轻松的将可迭代对象转换为数组。

# 生成器 (Generator)

- 什么是生成器？
  - 生成器是一个通过构造函数Generator创建的对象，生成器既是一个迭代器，同时又是一个可迭代对象
- 如何创建生成器？
  - 生成器的创建，必须使用生成器函数（Generator Function）
- 如何书写一个生成器函数？

```javascript
//这是一个生成器函数，该函数一定返回一个生成器
function *method(){
}
function* text(){
    console.log('开始');
    yield 1;
    console.log('第一次');
    yield 2;
    console.log('第二次');
    yield 3;
    console.log('第三次');
} 
const tex = text();
tex.next();
```

- 生成器函数内部是如何执行的？
  - 生成器函数内部是为了给生成器的每次迭代提供的数据
  - 每次调用生成器的next方法，将导致生成器函数运行到下一个yield关键字位置
  - yield是一个关键字，该关键字只能在生成器函数内部使用，表达“产生”一个迭代数据
- 有哪些需要注意的细节？
  - 生成器函数可以有返回值，返回值出现在第一次done为true时的value属性中
  - 调用生成器的next方法时，可以传递参数，传递的参数会交给yield表达式的返回值
  - 第一次调用next方法时，传参没有任何意义
  - 在生成器函数内部，可以调用其他生成器函数，但是要注意加上*号
  - 生成器函数返回的一定是一个可迭代对象
- 生成器的其他API
  - return方法：调用该方法，可以提前结束生成器函数，从而提前让整个迭代过程结束
  - throw方法：调用该方法，可以在生成器中产生一个错误

# 创建伪数组并使用数组方法

```javascript
const elems = { // 创建伪数组并使用数组方法，数组的本质就是一个对象
    length: 0,
    add: function(elem){
        Array.prototype.push.call(this, elem);
    },
    gather: function(num){
        this.add(num);
    },
    find: function(callback){
        return Array.prototype.find.call(this, callback);
    }
};
elems.add(1);
elems.add(2);
elems.add(3);
elems.add(4);
console.log(elems[2])
console.log(elems.find(i => i === 3))
```

# Set 集合

> 一直以来，JS只能使用数组和对象来保存多个数据，缺乏像其他语言那样拥有丰富的集合类型。因此，ES6新增了两种集合类型（set 和 map），用于在不同的场景中发挥作用。

**set用于存放不重复的数据**

- 如何创建set集合

```javascript
new Set(); //创建一个没有任何内容的set集合
new Set(iterable); //创建一个具有初始内容的set集合，内容来自于可迭代对象每一次迭代的结果
//数组去重
let arr = [1,2,3,2,3,4,3,1,2,3,5,6,7,8,6,45,4,3];
const result = [...new Set(arr)];
console.log(result);
//字符串去重
let str = "asdfasdescff132432343dfdssxswed";
const result2 = [...new Set(str)].join("");
console.log(result2);
const arr1 = [1,2,3,4,2,4,56,6,3,1,2,4,3,5];
const arr2 = [0,97,6,7,5,3,7,8,56,7,8,4,6,3,5,6,7,8,9];
console.log('并集',[...new Set([...arr1, ...arr2])]);
const cross = [...new Set(arr1)].filter(item => arr2.indexOf(item) >= 0);
console.log('交集',cross);
console.log('差集',[...new Set([...arr1, ...arr2])].filter(item => cross.indexOf(item) < 0));
```

- 如何对set集合进行后续操作
  - add(数据): 添加一个数据到set集合末尾，如果数据已存在，则不进行任何操作 
    - set使用Object.is的方式判断两个数据是否相同，但是，针对+0和-0，set认为是相等
  - has(数据): 判断set中是否存在对应的数据
  - delete(数据)：删除匹配的数据，返回是否删除成功
  - clear()：清空整个set集合
  - size: 获取set集合中的元素数量，只读属性，无法重新赋值
- 如何与数组进行相互转换

```javascript
const s = new Set([x,x,x,x,x]);
// set本身也是一个可迭代对象，每次迭代的结果就是每一项的值
const arr = [...s];
```

- 如何遍历
  - 使用for-of循环
  - 使用set中的实例方法forEach

注意：set集合中不存在下标，因此forEach中的回调的第二个参数和第一个参数是一致的，均表示set中的每一项

## 并集

把两个数组合并成同一个数据传入 Set 中求并集

```javascript
const ninjas = ["Kuma", "Hattori", "Yagyu"];
const samurai = ["Hattori", "Oda", "Tomoe"];

const warriors = new Set([...ninjas, ...samurai]); // 求并集
console.log(warriors)
```

## 交集

求两个数组中相同的数据集合

```javascript
const ninjas = new Set(["Kuma", "Hattori", "Yagyu"]);
const samurai = new Set(["Hattori", "Oda", "Tomoe"]);

const ninjaSamurais = new Set(
    [...ninjas].filter(ninja => samurai.has(ninja)) // 求交集
);
console.log(ninjaSamurais)
```

## 差集

求 A、B 两个数组中只存在在 A 数组不存在在 B 数组的数据集合

```javascript
const ninjas = new Set(["Kuma", "Hattori", "Yagyu"]);
const samurai = new Set(["Hattori", "Oda", "Tomoe"]);

const pureNinjas = new Set(
    [...ninjas].filter(ninja => !samurai.has(ninja)) // 求差集
);
console.log(pureNinjas)
```

# Map集合

- 键值对（key value pair）数据集合的特点：键不可重复
- map集合专门用于存储多个键值对数据。
- 在map出现之前，我们使用的是对象的方式来存储键值对，键是属性名，值是属性值。
- 使用对象存储有以下问题：
  - 键名只能是字符串 
  - 获取数据的数量不方便 
  - 键名容易跟原型上的名称冲突 
- 如何创建map

```javascript
new Map(); //创建一个空的map
new Map(iterable); //创建一个具有初始内容的map，初始内容来自于可迭代对象每一次迭代的结果，但是，它要求每一次迭代的结果必须是一个长度为2的数组，数组第一项表示键，数组的第二项表示值
let map1 = new Map([['a',1],['b',2],['c',3]]);
console.log(map1);
```

- 如何进行后续操作
  - size：只读属性，获取当前map中键的数量
  - set(键, 值)：设置一个键值对，键和值可以是任何类型 
    - 如果键不存在，则添加一项
    - 如果键已存在，则修改它的值
    - 比较键的方式和set相同
  - get(键): 根据一个键得到对应的值
  - has(键)：判断某个键是否存在
  - delete(键)：删除指定的键
  - clear(): 清空map
- 和数组互相转换
  - 和set一样
- 遍历
  - for-of，每次迭代得到的是一个长度为2的数组
  - forEach，通过回调函数遍历 
    - 参数1：每一项的值
    - 参数2：每一项的键
    - 参数3：map本身

# WeakSet 和 WeakMap

## WeakSet

使用该集合，可以实现和set一样的功能，不同的是：

- **它内部存储的对象地址不会影响垃圾回收**
- 只能添加对象
- 不能遍历（不是可迭代的对象）、没有size属性、没有forEach方法

## WeakMap

类似于map的集合，不同的是：

- **它的键存储的地址不会影响垃圾回收**
- 它的键只能是对象
- 不能遍历（不是可迭代的对象）、没有size属性、没有forEach方法

# 属性描述符

- Property Descriptor 属性描述符  是一个普通对象，用于描述一个属性的相关信息
- 通过`Object.getOwnPropertyDescriptor(对象, '属性名')`可以得到一个对象的某个属性的属性描述符
- 描述符：
  - value：属性值
  - configurable：该属性的描述符是否可以修改
  - enumerable：该属性是否可以被枚举
  - writable：该属性是否可以被重新赋值

> `Object.getOwnPropertyDescriptors(对象)`可以得到某个对象的所有属性描述符

如果需要为某个对象添加属性时 或 修改属性时， 配置其属性描述符，可以使用下面的代码:

```javascript
Object.defineProperty(对象, 属性名, {描述符});
Object.defineProperties(对象, {多个属性的描述符 a: {描述符}, b: {描述符} })
```

# 存取器属性

- 属性描述符中，如果配置了 get 和 set 中的任何一个，则该属性，不再是一个普通属性，而变成了存取器属性。
- get 和 set配置均为函数，如果一个属性是存取器属性，则读取该属性时，会运行get方法，将get方法得到的返回值作为属性值；如果给该属性赋值，则会运行set方法。
- 存取器属性最大的意义，在于可以控制属性的读取和赋值。

```html
<p>
  <span>姓名：</span>
  <span id="name"></span>
</p>
<p>
  <span>年龄：</span>
  <span id="age"></span>
</p>
<script>
  const spanName = document.getElementById("name")
  const spanAge = document.getElementById("age")
  const user = {}
  Object.defineProperties(user, {
    name: {
      get() {
        return spanName.innerText;
      },
      set(val) {
        spanName.innerText = val;
      }
    },
    age: {
      get() {
        return +spanAge.innerText;
      },
      set(val) {
        if (typeof val !== "number") {
          throw new TypeError("年龄必须是一个数字")
        }
        if (val < 0) {
          val = 0;
        } else if (val > 200) {
          val = 200;
        }
        spanAge.innerText = val;
      }
    }
  })
</script>
```

# Reflect

- Reflect是什么？
  - Reflect是一个内置的JS对象，它提供了一系列方法，可以让开发者通过调用这些方法，访问一些JS底层功能
  - 由于它类似于其他语言的**反射**，因此取名为Reflect
- 它可以做什么？
  - 使用Reflect可以实现诸如 属性的赋值与取值、调用普通函数、调用构造函数、判断属性是否存在与对象中  等等功能
- 这些功能不是已经存在了吗？为什么还需要用Reflect实现一次？
  - 有一个重要的理念，在ES5就被提出：减少魔法、让代码更加纯粹
  - 这种理念很大程度上是受到函数式编程的影响
  - ES6进一步贯彻了这种理念，它认为，对属性内存的控制、原型链的修改、函数的调用等等，这些都属于底层实现，属于一种魔法，因此，需要将它们提取出来，形成一个正常的API，并高度聚合到某个对象中，于是，就造就了Reflect对象
  - 因此，你可以看到Reflect对象中有很多的API都可以使用过去的某种语法或其他API实现。
- 它里面到底提供了哪些API呢？
  - Reflect.set(target, propertyKey, value): 设置对象target的属性propertyKey的值为value，等同于给对象的属性赋值
  - Reflect.get(target, propertyKey): 读取对象t arget的属性propertyKey，等同于读取对象的属性值
  - Reflect.apply(target, thisArgument, argumentsList)：调用一个指定的函数，并绑定this和参数列表。等同于函数调用
  - Reflect.deleteProperty(target, propertyKey)：删除一个对象的属性
  - Reflect.defineProperty(target, propertyKey, attributes)：类似于Object.defineProperty，不同的是如果配置出现问题，返回false而不是报错
  - Reflect.construct(target, argumentsList)：用构造函数的方式创建一个对象
  - Reflect.has(target, propertyKey): 判断一个对象是否拥有一个属性
  - 其他API：[https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect)

# Proxy 代理

代理：提供了修改底层实现的方式

```javascript
//代理一个目标对象
//target：目标对象
//handler：是一个普通对象，其中可以重写底层实现
//返回一个代理对象
new Proxy(target, handler)
<script>
  const obj = {
    a: 1,
    b: 2
  }
const proxy = new Proxy(obj, {
  set(target, propertyKey, value) {
    // console.log(target, propertyKey, value);
    // target[propertyKey] = value;
    Reflect.set(target, propertyKey, value);
  },
  get(target, propertyKey) {
    if (Reflect.has(target, propertyKey)) {
      return Reflect.get(target, propertyKey);
    } else {
      return -1;
    }
  },
  has(target, propertyKey) {
    return false;
  }
});
// console.log(proxy);
// proxy.a = 10;
// console.log(proxy.a);
console.log(proxy.d);
console.log("a" in proxy);
</script>
```

```javascript
const obj = { name: 'Tom' }
const objPro = new Proxy(obj, {
    get(target: { name: string }, key: string | symbol, receiver: any): any {
        console.log(target, key, receiver)
        return key in target ? target[key] : null
    },
    set(target: { name: string }, key: string | symbol, value: any): any {
        console.log(target, key, value)
        target[key] = value;
    }
})
objPro.name = 'this'
objPro.name
console.log(objPro.name)
```

## 将一个对象修改为代理对象

```javascript
function makeLoggable(target){
    return new Proxy(target, {
        get: (target, property) => {
            return target[property];
        },

        set: (target, property, value) => {
            target[property] = value;
        }
    });
}

let ninja = { name: "Yoshi"}; // 该对象依旧活跃，只不过被代理对象给代理了
ninja = makeLoggable(ninja); // 获取代理对象，vue3的响应式原理

ninja.weapon = "sword";
console.log(ninja)

```

## 使用代理记录日志

```javascript
function makeLoggable(target){
    let count = 1;
    return new Proxy(target, {
        get: (target, property) => {
            console.log(target + '的属性被访问了！' + count + '次')
            count++
            return target[property];
        },

        set: (target, property, value) => {
            console.log(target + '的' + property + '属性的值从' + target[property] + '被修改为' + value)
            target[property] = value;
        }
    });
}

let ninja = { name: "Yoshi"};
ninja = makeLoggable(ninja);

ninja.weapon = "sword";
console.log(ninja, ninja.name, ninja.weapon, ninja.name, ninja.weapon)

```

## 使用代理包装函数并评估性能

```javascript
function isPrime(number){
    if(number < 2) { return false; }

    for(let i = 2; i < number; i++) {
        if(number % i === 0) { return false; }
    }

    return true;
}

isPrime = new Proxy(isPrime, {
    apply: (target, thisArg, args) => { // 原函数，调用原函数时的this指向，参数数组
        console.log(target, thisArg, args)
        console.time("isPrime");

        const result = target.apply(thisArg, args);

        console.timeEnd("isPrime");

        return result;
    }
});

console.log(isPrime.call(global, 1299827))
```

## 使用代理自动填充属性

```javascript
function Folder() {
    return new Proxy({}, {
        get: (target, property) => {
            if(!(property in target)) { // 如果属性不存在就创建属性
                target[property] = new Folder();
            }

            return target[property];
        },
        set: (target, property, value) => {
            target[property] = value;
        }
    });
}

const rootFolder = new Folder();
rootFolder.ninjasDir.firstNinjaDir.ninjaFile = "yoshi.txt"; // 层层读取，读取到最后一个转为设置
console.log(rootFolder) // { ninjasDir: { firstNinjaDir: { ninjaFile: 'yoshi.txt' } } }
```

### 代理中没有设置 getter 和 setter 时默认使用对象的读取和赋值操作

```javascript
let obj = { a: 2 }
objPro = new Proxy(obj, {})
console.log(obj.a, objPro.a) // 2, 2
objPro.a = 3;
console.log(obj.a, objPro.a) // 3, 3
```

## 使用代理实现数组的负索引

```javascript
function createNegativeArrayProxy(array){
    if (!Array.isArray(array)) {
        throw new TypeError('Expected an array');
    }

    return new Proxy(array, {
        get: (target, index) => {
            console.log(target, index)
            index = +index; // 使用一元操作符 + 将字符串索引改为数字
            return target[index < 0 ? target.length + index : index]; // 根据正负下标获取数据
        },
        set: (target, index, val) => {
            console.log(target, index, val)
            index = +index;
            return target[index < 0 ? target.length + index : index] = val;
        }
    });
}

let ninjas = ["Yoshi", "Kuma", "Hattori"];
ninjas = createNegativeArrayProxy(ninjas);
console.log(ninjas, ninjas[0], ninjas[2], ninjas[-1])
```

## 使用代理实现观察者模式

有一个对象，是观察者，它用于观察另外一个对象的属性值变化，当属性值变化后会收到一个通知，可能会做一些事。

```javascript
<script>
  //创建一个观察者
  function observer(target) {
  const div = document.getElementById("container");
  const proxy = new Proxy(target, {
    set(target, prop, value) {
      Reflect.set(target, prop, value);
      render();
    },
    get(target, prop){
      return Reflect.get(target, prop);
    }
  })
  render();
  function render() {
    let html = "";
    for (const prop of Object.keys(target)) {
      html += `
                    <p><span>${prop}：</span><span>${target[prop]}</span></p>
                `;
    }
    div.innerHTML = html;
  }

  return proxy;
}
const target = {
  a: 1,
  b: 2
}
const obj = observer(target)
</script>
//构造函数模型
<script>
      class User {

      }
function ConstructorProxy(Class, ...propNames) {
  return new Proxy(Class, {
    construct(target, argumentsList) {
      const obj = Reflect.construct(target, argumentsList)
      propNames.forEach((name, i) => {
        obj[name] = argumentsList[i];
      })
      return obj;
    }
  })
}
const UserProxy = ConstructorProxy(User, "firstName", "lastName", "age")
const obj = new UserProxy("袁", "进", 18);
console.log(obj)
class Monster {
}
const MonsterProxy = ConstructorProxy(Monster, "attack", "defence", "hp", "rate", "name")
const m = new MonsterProxy(10, 20, 100, 30, "怪物")
console.log(m);
</script>
//验证函数参数
<script>
  function sum(a, b) {
  return a + b;
}
function validatorFunction(func, ...types) {
  return function(...argumentsList) {
    types.forEach((t, i) => {
      const arg = argumentsList[i]
      if (typeof arg !== t) {
        throw new TypeError(`第${i+1}个参数${argumentsList[i]}不满足类型${t}`);
      }
    })
    return func(...argumentsList)
  }
  return proxy;
}
const sumProxy = validatorFunction(sum, "number", "number")
console.log(sumProxy(1, 2))
</script>
```

# 新增的数组API

## 静态方法

- Array.of(...args): 使用指定的数组项创建一个新数组
- Array.from(arg): 通过给定的类数组 或 可迭代对象 创建一个新的数组。

## 实例方法

- find(callback): 用于查找满足条件的第一个元素
- findIndex(callback)：用于查找满足条件的第一个元素的下标
- fill(data)：用指定的数据填充满数组所有的内容
- copyWithin(target, start?, end?): 在数组内部完成复制,从目标下标开始改变，从开始位置进行复制，在结束位置复制停止，后两个参数可以不传，默认从头复制，复制到目标下标前一个数据
- includes(data)：判断数组中是否包含某个值，使用Object.is匹配

## 类型化数组

### 数字存储的前置知识

-  计算机必须使用固定的位数来存储数字，无论存储的数字是大是小，在内存中占用的空间是固定的。 
-  n位的无符号整数能表示的数字是2^n个，取值范围是：0 ~ 2^n - 1 
-  n位的有符号整数能表示的数字是2n个，取值范围是：-2(n-1) ~ 2^(n-1) - 1 
-  浮点数表示法可以用于表示整数和小数，目前分为两种标准： 
   - 32位浮点数：又称为单精度浮点数，它用1位表示符号，8位表示阶码，23位表示尾数
   - 64位浮点数：又称为双精度浮点数，它用1位表示符号，11位表示阶码，52位表示尾数
-  JS中的所有数字，均使用双精度浮点数保存 

### 类型化数组

- 类型化数组：用于优化多个数字的存储，只针对数字
- 具体分为：
  - Int8Array： 8位有符号整数（-128 ~ 127）
  - Uint8Array： 8位无符号整数（0 ~ 255）
  - Int16Array: ...
  - Uint16Array: ...
  - Int32Array: ...
  - Uint32Array: ...
  - Float32Array:
  - Float64Array
- 如何创建数组

```javascript
new 数组构造函数(长度)
new Int8Array(10);
数组构造函数.of(元素...)
Int8Array.of(1,3,4,5 )
数组构造函数.from(可迭代对象)
new 数组构造函数(其他类型化数组)
```

- 得到长度
  - 数组.length   //得到元素数量
  - 数组.byteLength //得到占用的字节数
- 其他的用法跟普通数组一致，但是：
  - 不能增加和删除数据，类型化数组的长度固定
  - 一些返回数组的方法，返回的数组是同类型化的新数组

# ArrayBuffer

ArrayBuffer：一个对象，用于存储一块固定内存大小的数据。

```javascript
new ArrayBuffer(字节数)
new ArrayBuffer(10) // 存储10个字节的空间
```

可以通过属性`byteLength`得到字节数，可以通过方法`slice`得到新的ArrayBuffer

## 读写ArrayBuffer

- 使用DataView
  - 通常会在需要混用多种存储格式时使用DataView`new DataView(字节数,偏移量，操作的数量 )`
- 使用类型化数组
  - 实际上，每一个类型化数组都对应一个ArrayBuffer，如果没有手动指定ArrayBuffer，类型化数组创建时，会新建一个ArrayBuffer