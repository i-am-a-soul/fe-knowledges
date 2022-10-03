方法 - forEach()
===

> Create by **jsliang** on **2019-09-17 09:34:13**  
> Recently revised in **2019-09-17 09:34:22**

* **原文**：[MDN - forEach()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

* **功能**：`forEach()` 方法对数组的每个元素执行一次提供的函数。

* **语法**：`arr.forEach(callback)`
  * `callback`：为数组中每个元素执行的函数，该函数接收三个参数：
    * `currentValue`：数组中当前正在处理的元素
    * `index`：数组中正在处理的当前元素的索引。
    * `array`：`forEach()` 方法正在操作的数组。

* **返回值**：`undefined`.

* **代码**：

```js
const items = ['item1', 'item2', 'item3'];
const copy = [];

// 使用 for 遍历
for (let i = 0; i < items.length; i++) {
  copy.push(items[i]);
}

// 使用 forEach 遍历
items.forEach(function(item){
  copy.push(item);
});
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

