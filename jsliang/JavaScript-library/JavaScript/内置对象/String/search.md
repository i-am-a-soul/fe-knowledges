方法 - search()
===

> Create by **jsliang** on **2019-09-11 17:01:23**  
> Recently revised in **2019-09-11 17:01:26**

* **原文**：[MDN - search()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/search)

* **功能**：`search()` 方法执行正则表达式和 `String` 对象之间的一个搜索匹配。

* **语法**：`str.search(regexp)`
  * `regexp`：正则表达式。

* **返回值**：如果匹配成功，则 `search()` 返回正则表达式在字符串中首次匹配项的索引;否则，返回 -1。

* **代码**：

```js
var str = "hey JudE";
var re = /[A-Z]/g;
var re2 = /[.]/g;
console.log(str.search(re)); // 4
console.log(str.search(re2)); // -1
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

