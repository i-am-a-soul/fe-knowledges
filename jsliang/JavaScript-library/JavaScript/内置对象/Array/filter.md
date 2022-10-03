方法 - filter()
===

> Create by **jsliang** on **2019-09-17 09:33:28**  
> Recently revised in **2019-09-17 09:33:40**

* **原文**：[MDN - filter()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

* **功能**：`filter()` 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。

* **语法**：`arr.filter(callback)`
  * `callback`：用来测试数组的每个元素的函数。返回 `true` 表示该元素通过测试，保留该元素，`false` 则不保留。它接受以下三个参数：
    * `element`：数组中当前正在处理的元素
    * `index`：正在处理的元素在数组中的索引。
    * `array`：调用了 `filter` 的数组本身。

* **返回值**：一个新的、由通过测试的元素组成的数组，如果没有任何数组元素通过测试，则返回空数组。

* **代码**：

```js
function isBigEnough(element) {
  return element >= 10;
}
var filtered = [12, 5, 8, 130, 44].filter(isBigEnough);
// [12, 130, 44]
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

