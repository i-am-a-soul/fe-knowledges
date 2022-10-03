Function
===

> Create by **jsliang** on **2019-10-15 22:18:16**  
> Recently revised in **2019-10-15 22:26:19**

* **原文**：[MDN - Function](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function)

* **功能**：`Function` 构造函数创建一个新的 `Function` 对象。在 JavaScript 中，每个函数实际上都是一个 `Function` 对象。

* **语法**：`new Function ([arg1[, arg2[, ...argN]],] functionBody)`
  * `arg1, arg2, ...argN`：被函数使用的参数的名称必须是合法命名的。参数名称是一个有效的 JavaScript 标识符的字符串，或者一个用逗号分隔的有效字符串的列表;例如 '×'，'theValue'，或 'A, B'。
  * `functionBody`：一个含有包括函数定义的 JavaScript 语句的字符串。

* **属性对象**：

1. `Function.length`：获取函数的接收参数个数。
2. `Function.prototype.constructor`：声明函数的原型构造方法。

* **方法**：

1. `Function.prototype.apply()`：在一个对象的上下文中应用另一个对象的方法；参数能够以数组形式传入。
2. `Function.prototype.bind()`：`bind()` 方法会创建一个新函数，称为绑定函数。当调用这个绑定函数时，绑定函数会以创建它时传入 `bind()` 方法的第一个参数作为 `this`，传入 `bind()` 方法的第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。
3. `Function.prototype.call()`：在一个对象的上下文中应用另一个对象的方法；参数能够以列表形式传入。
4. `Function.prototype.toString()`：获取函数的实现源码的字符串。覆盖了 `Object.prototype.toString` 方法。

* **代码**：

```js
const adder = new Function('a', 'b', 'return a + b');
console.log(adder(2, 6)); // 8
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

