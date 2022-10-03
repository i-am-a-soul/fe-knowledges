方法 - findIndex()
===

> Create by **jsliang** on **2019-09-17 09:40:26**  
> Recently revised in **2019-09-17 09:40:37**

* **原文**：[MDN - findIndex()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)

* **功能**：`findIndex()` 方法返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1。

* **语法**：`arr.findIndex(callback)`
  * `callback`：在数组每一项上执行的函数，接收 3 个参数：
    * `element`：当前遍历到的元素。
    * `index`：当前遍历到的索引。
    * `array`：数组本身。

* **返回值**：返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1。

* **代码**：

```js
var array1 = [5, 12, 8, 130, 44];

function isLargeNumber(element) {
  return element > 13;
}

array1.findIndex(isLargeNumber); // 3
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

