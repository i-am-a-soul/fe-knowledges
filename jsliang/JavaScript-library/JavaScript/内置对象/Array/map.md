方法 - map()
===

> Create by **jsliang** on **2019-09-17 09:35:55**  
> Recently revised in **2019-09-17 09:36:04**

* **原文**：[MDN - map()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

* **功能**：`map()` 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

* **语法**：`map((item, index) => {})`
  * `item`：遍历的项
  * `index`：该次遍历项的索引

* **返回值**：一个新数组，每个元素都是回调函数的结果。

* **代码**：

```js
[1, 2, 3, 4].map(item => item * 2) // [2, 4, 6, 8]

[{
  name: 'jsliang',
  age: 24,
}, {
  name: '梁峻荣',
  age: 124
}].map((item, index) => {
  return `${index} - ${item.name}`;
}) // ['0 - jsliang', '1 - 梁峻荣']
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

