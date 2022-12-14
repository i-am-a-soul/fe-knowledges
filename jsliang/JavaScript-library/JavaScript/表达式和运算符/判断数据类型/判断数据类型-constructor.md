判断数据类型 - constructor
===

> Create by **jsliang** on **2019-10-16 01:23:30**  
> Recently revised in **2019-10-16 01:23:33**

* **原文**：[MDN - constructor](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor)

* **功能**：`constructor` 返回创建实例对象的 Object 构造函数的引用。

* **描述**：

所有对象都会从它的原型上继承一个 `constructor` 属性。

```js
const arr = [];
console.log(arr.constructor === Array); // true

const obj = {};
console.log(obj.constructor === Object); // true

const num = 1;
console.log(num.constructor === Number); // true

const str = '1';
console.log(str.constructor === String); // true

const bool = true;
console.log(bool.constructor === Boolean); // true

const nul = null;
// console.log(nul.constructor); // 报错：Uncaught TypeError: Cannot read property 'constructor' of null at <anonymous>:1:5

const undefin = undefined;
// console.log(undefin.constructor); // 报错：Uncaught TypeError: Cannot read property 'constructor' of null at <anonymous>:1:5
```

* **说明**：

本次我们了解的，是通过 `constructor` 来判断某个数据的类型：

* [判断数据类型-方法合集](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%92%8C%E8%BF%90%E7%AE%97%E7%AC%A6/%E5%88%A4%E6%96%AD%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B-%E6%96%B9%E6%B3%95%E5%90%88%E9%9B%86.md)

在这篇文章中，我们会通过 `typeof`、`instanceof`、`constructor` 以及 `Object.prototype.toString().call()` 这四个方法，讲解这些方法判断数据类型的情况。

但是 `constructor` 的功能不限于此，更多的我们就后续进行跟进了。

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

