方法 - lastIndexOf()
===

> Create by **jsliang** on **2019-09-17 09:35:29**  
> Recently revised in **2019-09-17 09:35:38**

* **原文**：[MDN - lastIndexOf()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf)

* **功能**：`lastIndexOf()` 方法返回指定元素（也即有效的 JavaScript 值或变量）在数组中的最后一个的索引，如果不存在则返回 -1。

* **语法**：`lastIndexOf(searchValue, fromIndex)`
  * `searchValue`：查找的值
  * `formIndex`：从该位置逆向查找

* **返回值**：数组中最后一个元素的索引，如未找到返回 -1。

* **代码**：

```js
var array = [2, 5, 9, 2];
var index = array.lastIndexOf(2); // 3
```

* **扩展**：如果需要查找到第一次出现指定值的索引，可以使用 `indexOf()`。

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

