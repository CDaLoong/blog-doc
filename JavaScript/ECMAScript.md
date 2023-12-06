## 概述
HTML 定义网页的结构与内容，CSS 定义其格式与样式，而 JavaScript 则为网页增加可交互性，创作功能丰富的 Web 应用。
但是，如果从浏览器的范畴去理解“JavaScript”这个术语，它包含了截然不同的两个方面。一方面是 JavaScript 的核心语言（ECMAScript），另一方面是大量的 Web API (en-US)，包括 DOM（文档对象模型）。
JavaScript 的核心语言是 ECMAScript，是一门由 ECMA TC39 委员会标准化的编程语言。“ECMAScript”是语言标准的术语，但“ECMAScript”和“JavaScript”是可以互换使用的。该核心语言同样可以被用在非浏览器环境之中，例如 Node.js。

除却一些其他元素，ECMAScript 定义了：
- 语法（解析规则、关键词、流程控制、对象初始化，等等）
- 错误处理机制（throw、try...catch，以及创建用户自定义错误类型的能力）
- 类型（布尔值、数字、字符串、函数、对象，等等）
- 基于原型的继承机制
- 内置对象和函数（JSON、Math、Array 方法、parseInt、decodeURI，等等）
- 严格模式
- 模块系统
- 基本内存模型

### 标准化流程
ECMAScript 版本由每年的 ECMA 大会批准并作为标准发布。所有的进展都在 Ecma TC39 GitHub 组织上公开，该组织托管提案、官方规范文本和会议记录。
在 ECMAScript 第 6 版（称为 ES6）之前，规范是几年发布一次，通常用它们的主要版本号来指代（ES3、ES5 等）。在 ES6 之后，规范以发布年份命名（ES2017、ES2018 等）。ES6 是 ES2015 的代名词。ESNext 是一个动态名称，指的是撰写本文时的下一个版本。ESNext 中的特性更准确地称为提案，因为根据定义，规范尚未最终确定。
目前委员会批准的 ECMA-262 的快照有 PDF 版本和 HTML 版本。ECMA-262 和 ECMA-402 正处于维护状态，仍在由规范编辑者更新；TC39 网站托管了最新版本的 ECMA-262 和 ECMA-402。
新的语言特性，包括新的语法和 API 的引入以及现有行为的修订，都以提案的形式进行讨论。每个提案都需要经过 4 个阶段的过程，通常在第 3 或 第 4 阶段时，JavaScript 引擎会实现这些提案，以供公众使用。

## ECMAScript2023+ 新特性

### 数组的新方法

- Array.prototype.findLast()
findLast() 是一个迭代方法。该方法对数组每一个元素按降序（索引从大到小）执行 callbackFn 函数，直到 callbackFn 返回一个真值。然后 findLast() 返回该元素的值并停止遍历数组。如果 callbackFn 没有返回一个真值，则 findLast() 返回 undefined。

- Array.prototype.findLastIndex()
findLastIndex() 方法是一个迭代方法。它为数组中的每个元素按索引降序调用一次提供的 callbackFn 函数，直到 callbackFn 返回一个真值。然后 findLastIndex() 返回元素的索引并且停止遍历数组。如果 callbackFn 没有返回一个真值，则 findLastIndex() 返回 -1。


```js
Array.prototype.toReversed() // 该方法返回一个新数组，新数组的元素顺序与原数组相反。
Array.prototype.toSorted(compareFn) // 该方法返回一个新数组，新数组的元素是原数组元素的排序结果。
Array.prototype.toSpliced(start, deleteCount, ...items) // 该方法返回一个新数组，新数组删除了原数组从指定位置开始的指定数量的元素。
Array.prototype.with(index, value) // 该方法返回一个新数组，新数组在指定索引位置的元素被替换为指定值。
```
