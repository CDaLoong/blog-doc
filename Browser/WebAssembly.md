## 概述
WebAssembly 是一种运行在现代网络浏览器中的新型代码，并且提供新的性能特性和效果。它设计的目的不是为了手写代码而是为诸如 C、C++ 和 Rust 等低级源语言提供一个高效的编译目标。

对于网络平台而言，这具有巨大的意义——这为客户端 app 提供了一种在网络平台以接近本地速度的方式运行多种语言编写的代码的方式；在这之前，客户端 app 是不可能做到的。

而且，你在不知道如何编写 WebAssembly 代码的情况下就可以使用它。WebAssembly 的模块可以被导入的到一个网络 app（或 Node.js）中，并且暴露出供 JavaScript 使用的 WebAssembly 函数。JavaScript 框架不但可以使用 WebAssembly 获得巨大性能优势和新特性，而且还能使得各种功能保持对网络开发者的易用性。

特点：
- 快速、高效、可移植——通过利用常见的硬件能力，WebAssembly 代码在不同平台上能够以接近本地速度运行。
- 可读、可调试——WebAssembly 是一门低阶语言，但是它有确实有一种人类可读的文本格式（其标准即将得到最终版本），这允许通过手工来写代码，看代码以及调试代码。
- 保持安全——WebAssembly 被限制运行在一个安全的沙箱执行环境中。像其他网络代码一样，它遵循浏览器的同源策略和授权策略。
- 不破坏网络——WebAssembly 的设计原则是与其他网络技术和谐共处并保持向后兼容。

网络平台(浏览器/webview)可以被想象成拥有两个部分：
1. 一个运行网络程序（Web app）代码——比如，给你的程序提供能力的 JavaScript——的虚拟机
2. 一系列网络程序能够调用从而控制网络浏览器/设备功能，并且能够让事物发生变化的网络 API（DOM、CSSOM、WebGL、IndexedDB、Web Audio API等）

从历史角度讲，虚拟机过去只能加载 JavaScript。这对我们而言足够了，因为 JavaScript 足够强大从而能够解决人们在当今网络上遇到的绝大部分问题。尽管如此，当试图把 JavaScript 应用到诸如 3D 游戏、虚拟现实、增强现实、计算机视觉、图像/视频编辑以及大量的要求原生性能的其他领域的时候，就会遇到性能问题。而且，下载、解析以及编译巨大的 JavaScript 应用程序的成本是过高的。移动平台和其他资源受限平台进一步放大了这些性能瓶颈。

WebAssembly 是一门不同于 JavaScript 的语言，但是，它不是用来取代 JavaScript 的。相反，它被设计为和 JavaScript 一起协同工作，从而使得网络开发者能够利用两种语言的优势：
1. JavaScript 是一门高级语言。对于写网络应用程序而言，它足够灵活且富有表达力。它有许多优势——它是动态类型的，不需要编译环节以及一个巨大的能够提供强大框架、库和其他工具的生态系统。
2. WebAssembly 是一门低级的类汇编语言。它有一种紧凑的二进制格式，使其能够以接近原生性能的速度运行，并且为诸如 C++ 和 Rust 等拥有低级的内存模型语言提供了一个编译目标以便它们能够在网络上运行。（注意，WebAssembly 有一个在将来支持使用了垃圾回收内存模型的语言的高级目标。）

随着 WebAssembly 出现在了浏览器中，我们前面提到的虚拟机将会加载和运行两种类型的代码——JavaScript 和 WebAssembly。

不同类型的代码能够按照需要进行相互调用——WebAssembly 的 JavaScript API 使用能够被正常调用的 JavaScript 函数封装了导出的 WebAssembly 代码，并且 WebAssembly 代码能够导入和同步调用常规的 JavaScript 函数。事实上，WebAssembly 代码的基本单元被称作一个模块，并且 WebAssembly 的模块在很多方面都和 ES2015 的模块是等价的。

### 关键概念

1. 模块：表示一个已经被浏览器编译为可执行机器码的 WebAssembly 二进制代码。一个模块是无状态的，并且像一个二进制大对象（Blob）一样能够被缓存到 IndexedDB 中或者在 window 和 worker 之间进行共享（通过 postMessage() (en-US) 函数）。一个模块能够像一个 ES2015 的模块一样声明导入和导出。
2. 内存：ArrayBuffer，大小可变。本质上是连续的字节数组，WebAssembly 的低级内存存取指令可以对它进行读写操作。
3. 表格：带类型数组，大小可变。表格中的项存储了不能作为原始字节存储在内存里的对象的引用（为了安全和可移植性的原因）。
4. 实例：一个模块及其在运行时使用的所有状态，包括内存、表格和一系列导入值。一个实例就像一个已经被加载到一个拥有一组特定导入的特定的全局变量的 ES2015 模块。

JavaScript API 为开发者提供了创建模块、内存、表格和实例的能力。给定一个 WebAssembly 实例，JavaScript 代码能够调用普通 JavaScript 函数暴露出来的导出代码。通过把 JavaScript 函数导入到 WebAssembly 实例中，任意的 JavaScript 函数都能被 WebAssembly 代码同步调用。

因为 JavaScript 能够完全控制 WebAssembly 代码如何下载、编译运行，所以，JavaScript 开发者甚至可以把 WebAssembly 想象成一个高效地生成高性能函数的 JavaScript 特性。

将来，WebAssembly 模块将会像 ES2015 模块那样加载（使用`<script type='module'>`)，这也就意味着 JavaScript 代码能够像轻松地使用一个 ES2015 模块那样来获取、编译和导入一个 WebAssembly 模块。


## WebAssembly

WebAssembly JavaScript 对象是所有 WebAssembly 相关功能的命名空间。和大多数全局对象不一样，WebAssembly不是一个构造函数（它不是一个函数对象）。它类似于 Math 对象或者 Intl 对象，Math 对象也是一个命名空间对象，用于保存数学常量和函数；Intl 则是用于国际化和其他语言相关函数的命名空间对象。

WebAssembly 对象主要用于：

1. 使用 `WebAssembly.instantiate()` 函数加载 WebAssembly 代码。
2. 通过 `WebAssembly.Memory()/WebAssembly.Table()` 构造函数创建新的内存和表实例。
3. 由 `WebAssembly.CompileError()/WebAssembly.LinkError() (en-US)/WebAssembly.RuntimeError()` 构造函数来提供 WebAssembly 中的错误信息。


### 方法

- `WebAssembly.instantiate()`: 用于编译和实例化 WebAssembly 代码的主 API，返回一个 Module 和它的第一个Instance实例。

- `WebAssembly.instantiateStreaming()`: 直接从流式底层源编译和实例化 WebAssembly 模块，同时返回Module及其第一个Instance实例。

- `WebAssembly.compile()`: 把 WebAssembly 二进制代码编译为一个 WebAssembly.Module ，不进行实例化。

- `WebAssembly.compileStreaming()` :直接从流式底层源代码编译WebAssembly.Module ，将实例化作为一个单独的步骤。

- `WebAssembly.validate()`: 校验 WebAssembly 二进制代码的类型数组是否合法，合法则返回 true，否则返回 false。

### 构造器

- `WebAssembly.Global()`: 创建一个新的 WebAssembly Global 全局对象。

- `WebAssembly.Module()`: 创建一个新的 WebAssembly Module模块对象。

- `WebAssembly.Instance()`: 创建一个新的 WebAssembly Instance实例对象。

- `WebAssembly.Memory()`: 创建一个新的 WebAssembly Memory内存对象。

- `WebAssembly.Table()`: 创建一个新的 WebAssembly Table表格对象。

- `WebAssembly.CompileError()`: 创建一个新的 WebAssembly CompileError编译错误对象。

- `WebAssembly.LinkError() (en-US)`: 创建一个新的 WebAssembly LinkError链接错误对象。

- `WebAssembly.RuntimeError()`: 创建一个新的 WebAssembly RuntimeError运行时错误对象。