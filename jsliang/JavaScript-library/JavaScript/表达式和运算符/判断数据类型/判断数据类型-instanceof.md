判断数据类型 - instanceof
===

> Create by **jsliang** on **2019-10-15 19:50:51**  
> Recently revised in **2019-10-16 01:12:27**

* **原文**：[MDN - instanceof](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof)

* **功能**：`instanceof` 运算符用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链上。

* **示例**：

```js
function Car(make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
}
var auto = new Car('Honda', 'Accord', 1998);

console.log(auto instanceof Car); // true

console.log(auto instanceof Object); // true
```

* **方法**：`object instanceof constructor`
  * `object`：某个实例对象。
  * `constructor`：某个构造函数

* **说明**：

`instanceof` 运算符用来检测 `constructor.prototype` 是否存在于参数 `Object` 的原型链上。

同时，`instanceof` 运算符也可以用来判断数据类型，但是它会存在一点 “缺陷”，详细可观看代码。

* **代码**：

```js
/**
 * @name instanceof示例1
 * @description 检测字符串类型
 */
const simpleString = '这是简单的 String';
const newString = new String('这是 New 出来的 String');

console.log(simpleString instanceof String); // false，检查原型链会返回 undefined
console.log(newString instanceof String); // true

/**
 * @name instanceof示例2
 * @description 检测数字类型
 */
const simpleNumber = 123;
const newNumber = new Number(123);

console.log(simpleNumber instanceof Number); // false
console.log(newNumber instanceof Number); // true

/**
 * @name instanceof示例3
 * @description 检测对象类型
 */
const simpleOjbect = {};
const newObject = new Object();

console.log(simpleOjbect instanceof Object); // true
console.log(newObject instanceof Object); // true
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

