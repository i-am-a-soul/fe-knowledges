方法 - unshift()
===

> Create by **jsliang** on **2019-09-17 09:30:51**  
> Recently revised in **2019-09-17 09:30:54**

* **原文**：[MDN - unshift()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)

* **功能**：`unshift()` 方法将一个或多个元素添加到数组的开头，并返回该数组的新长度。

* **语法**：`arr.unshift(element1, ..., elementN)`
  * `element1`：要插入的第一个元素
  * `elementN`：要插入的第 N 个元素

* **返回值**：当一个对象调用该方法时，返回其 `length` 属性值。（ `unshift` 会改变原本数组）

* **代码**：

```js
let arrA = ['1'];
arrA.unshift('0');
console.log(arrA); // ['0', '1']

let arrB = [4, 5, 6];
arrB.unshift(1, 2, 3);
console.log(arrB); // [1, 2, 3, 4, 5, 6]
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

