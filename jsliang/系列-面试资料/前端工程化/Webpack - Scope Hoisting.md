Webpack - Scope Hoisting
===

> Create by **jsliang** on **2020-10-21 22:14:34**  
> Recently revised in **2020-12-06 20:26:53**

<!-- 目录开始 -->
## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- |
| [一 目录](#chapter-one) |
| [二 前言](#chapter-two) |
| [三 Scope Hoisting 开启前后对比](#chapter-three) |
| [四 原理](#chapter-four) |
| [五 参考文献](#chapter-five) |
<!-- 目录结束 -->

## 二 前言



`Scope Hoisting` 是 Webpack3 的新功能，直译为 **「作用域提升」**，它可以让 Webpack 打包出来的 **「代码文件更小」**，**「运行更快」**。

熟悉 JavaScript 都应该知道 **「函数提升」** 和 **「变量提升」** ，JavaScript 会把函数和变量声明提升到当前作用域的顶部。

**「作用域提升」** 也类似于此，Webpack 会把引入的 js 文件 “提升到” 它的引入者顶部。

## 三 Scope Hoisting 开启前后对比



假设我们有两个文件：

> 原始文件

```js
// main.js
export default "hello jsliang~";

// index.js
import str from "./main.js";
```

使用 Webpack 打包后输出文件内容：

```js
[
  (function (module, __webpack_exports__, __webpack_require__) {
    var __WEBPACK_IMPORTED_MODULE_0__util_js__ = __webpack_require__(1);
    console.log(__WEBPACK_IMPORTED_MODULE_0__util_js__["a"]);
  }),
  (function (module, __webpack_exports__, __webpack_require__) {
    __webpack_exports__["a"] = ('hello jsliang~');
  })
]
```

开启 Scope Hoisting 后输出文件内容：

```js
[
  (function (module, __webpack_exports__, __webpack_require__) {
    var util = ('hello jsliang~');
    console.log(util);
  })
]
```

对比两种打包方式输出的代码，我们可以看出，启用 `Scope Hoisting` 后，函数声明变成一个， `main.js` 中定义的内容被直接注入到 `main.js` 对应模块中，这样做的好处：

* 「代码体积更小」，因为函数申明语句会产生大量代码，导致包体积增大（模块越多越明显）；
* 代码在运行时因为创建的函数作用域更少，「内存开销也随之变小」。

## 四 原理



`Scope Hoisting` 的实现原理其实很简单：分析出模块之间的依赖关系，尽可能将打散的模块合并到一个函数中，前提是不能造成代码冗余。因此「只有那些被引用了一次的模块才能被合并」。

由于 `Scope Hoisting` 需要分析出模块之间的依赖关系，因此源码「必须采用 `ES6` 模块化语句」，不然它将无法生效。原因和 `Tree Shaking` 中介绍的类似。

## 五 参考文献



* [x] [webpack 的 scope hoisting 是什么？](https://ssshooter.com/2019-02-20-webpack-scope-hoisting/)【阅读建议：5min】
* [x] [通过Scope Hoisting优化Webpack输出](https://imweb.io/topic/5a43064fa192c3b460fce360)【阅读建议：5min】
* [x] [【Webpack】654- 了不起的 Webpack Scope Hoisting 学习指南](https://cloud.tencent.com/developer/article/1663231)【阅读建议：5min】

---


