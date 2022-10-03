方法 - sort()
===

> Create by **jsliang** on **2019-09-17 09:37:28**  
> Recently revised in **2019-09-17 09:37:39**

* **原文**：[MDN - sort()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

* **功能**：`sort()` 对数组的元素进行排序，并返回数组。

* **语法**：`sort(function)`
  * `function`：按某种顺序进行排列的函数。

* **返回值**：排序后的数组。

* **代码**：

```js
[4, 2, 5, 1, 3].sort(), // [1, 2, 3, 4, 5]
[4, 2, 5, 1, 3].sort((a, b) => a < b), // [5, 4, 3, 2, 1]
['a', 'd', 'c', 'b'].sort(), // ['a', 'b', 'c', 'd']
['jsliang', 'eat', 'apple'].sort(), // ['apple', 'eat', 'jsliang']
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

