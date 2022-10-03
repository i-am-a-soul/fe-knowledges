方法 - indexOf()
===

> Create by **jsliang** on **2019-09-17 09:35:04**  
> Recently revised in **2019-09-17 09:43:13**

* **原文**：[MDN - indexOf()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)

* **功能**：`indexOf()` 方法返回调用 String 对象中第一次出现的指定值的索引。

* **语法**：`indexOf(searchValue, fromIndex)`
  * `searchValue`：查找的值
  * `formIndex`：开始查找的位置

* **返回值**：如果找到了，则返回第一次出现的索引；如果没找到，则返回 `-1`。

* **代码**：

```js
'I am jsliang'.indexOf('a', 4); // 9
[1, 3, 1, 4].indexOf(1, 1); // 2
'怪盗 jsliang'.indexOf('我'); // -1
```

* **扩展**：如果需要查找到最后一次出现指定值的索引，可以使用 `lastIndexOf()`。

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

