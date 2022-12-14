方法 - fill()
===

> Create by **jsliang** on **2019-09-17 09:39:02**  
> Recently revised in **2019-09-17 09:39:12**

* **原文**：[MDN - fill()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)

* **功能**：`fill()` 方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。

* **语法**：`arr.fill(value, start, end)`
  * `value`：用来填充数组元素的值。
  * `start`：起始索引，默认值为0。
  * `end`：终止索引，默认值为 `this.length`。

* **返回值**：修改后的数组。

* **代码**：

```js
let arr = [1, 2, 3, 4, 5];
arr = new Array(arr.length).fill(0);
// arr - [0, 0, 0, 0, 0];
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

