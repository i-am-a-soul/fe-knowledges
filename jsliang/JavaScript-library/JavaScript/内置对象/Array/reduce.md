方法 - reduce()
===

> Create by **jsliang** on **2019-09-17 09:39:31**  
> Recently revised in **2019-09-17 09:39:41**

* **原文**：[MDN - reduce()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

* **功能**：`reduce()` 方法对数组中的每个元素执行一个由您提供的reducer函数(升序执行)，将其结果汇总为单个返回值。

* **语法**：`arr.reduce((prev, next) => { return prev + next }`
  * `prev`：数组前一项的值
  * `next`：数组后一项的值
  * `return`：`return` 出来的值，会被当成下一次的 `prev`

* **返回值**：函数累计处理的结果

* **代码**：

```js
[1, 2, 3, 4].reduce((prev, next) => {
  return prev + next;
}); // 10
['前端', 'pang', 'liang'].reduce((prev, next, index) => {
  return (index = 0 ? '-js' : '') + prev + 'js' + next;
}); // 前端-jspang-jsliang
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

