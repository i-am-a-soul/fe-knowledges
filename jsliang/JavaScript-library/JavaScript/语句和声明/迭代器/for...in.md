语句和声明 - 迭代器 - for...in
===

> create by **jsliang** on **2019-10-14 11:09:21**  
> Recently revised in **2019-10-14 11:57:57**

* **原文**：[MDN - for...in](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in)

* **功能**：`for...in` 语句以任意顺序遍历一个对象的除 `Symbol` 以外的可枚举属性。

* **语法**：`for (variable in object) { statement }`
  * `variable`：在每次迭代时，`variable` 会被赋值为不同的属性名。
  * `object`：非 `Symbol` 类型的可枚举属性被迭代的对象。

* **说明**：

`for...in` 循环只遍历可枚举属性。

像 `Array` 和 `Object` 使用内置构造函数所创建的对象都会继承自 `Object.prototype` 和 `String.prototype` 的不可枚举属性，例如 `String` 的 `indexOf()` 方法或 `Object` 的 `toString()` 方法。

循环将遍历对象本身的所有可枚举属性，以及对象从其构造函数原型中继承的属性（更接近原型链中对象的属性覆盖原型属性）。

通常，在迭代过程中最好不要在对象上进行添加、修改或者删除属性的操作，除非是对当前正在被访问的属性。

> 提示：`for...in` 不应该用于迭代一个 `Array`，其中索引顺序很重要。如果迭代访问顺序很重要时，最好使用 `for` 或者 `Array.prototype.forEach()` 或者 `for...of` 循环。

> 如果仅迭代对象本身的属性，可以使用 `getOwnPropertyNames()` 或者执行 `hasOwnProperty()` 来确定某属性是否是对象本身的属性。

* **代码**：

```js
// 案例 1
const obj1 = {
  a: 1,
  b: 2,
  c: 3,
};

for (let prop in obj1) {
  console.log('Object.' + prop + ' = ' + obj1[prop]);
}

/**
 * 'Object.a = 1'
 * 'Object.b = 2'
 * 'Object.c = 3'
*/

// 案例 2
const triangle = {
  a: 1,
  b: 2,
  c: 3,
};

function ColoredTriangle() {
  this.color = 'deepbluesky';
}

ColoredTriangle.prototype = triangle;

const obj2 = new ColoredTriangle();

for (let prop in obj2) {
  if (obj2.hasOwnProperty(prop)) {
    console.log(`Object.${prop} = ${obj2[prop]}`);
  }
}

/**
 * 'Object.color = deepbluesky'
*/
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

