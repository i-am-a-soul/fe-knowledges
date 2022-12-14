方法 - splice()
===

> Create by **jsliang** on **2019-09-17 09:32:28**  
> Recently revised in **2019-09-17 09:32:38**

* **原文**：[MDN - splice()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

* **功能**：`splice()` 方法通过删除或替换现有元素或者原地添加新的元素来修改数组,并以数组形式返回被修改的内容。此方法会改变原数组。

* **语法**：`array.splice(start, deleteCount, item1, item2, ...)`
  * `start`：指定修改的开始位置（从0计数）。
  * `deleteCount`：整数，表示要移除的数组元素的个数。
  * `item1, item2, ...`：要添加进数组的元素,从start 位置开始。如果不指定，则 splice() 将只删除数组元素。

* **返回值**：由被删除的元素组成的一个数组。如果只删除了一个元素，则返回只包含一个元素的数组。如果没有删除元素，则返回空数组。

* **代码**：

```js
var months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');

console.log(months);
// ['Jan', 'Feb', 'March', 'April', 'June']

months.splice(4, 1, 'May');

console.log(months);
// ['Jan', 'Feb', 'March', 'April', 'May']
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

