方法 - match()
===

> Create by **jsliang** on **2019-09-11 13:17:12**  
> Recently revised in **2019-09-11 13:20:30**

* **原文**：[MDN - match()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/match)

* **功能**：`match()` 方法检索返回一个字符串匹配正则表达式的的结果。

* **语法**：`str.match(regexp)`
  * `regexp`：一个正则表达式对象。

* **返回值**：返回匹配的结果

* **代码**：

```js
var str = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
var regexp = /[A-E]/gi;
var matches_array = str.match(regexp);
//  ['A', 'B', 'C', 'D', 'E', 'a', 'b', 'c', 'd', 'e']
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

