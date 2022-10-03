方法 - matchAll()
===

> Create by **jsliang** on **2019-09-11 13:21:27**  
> Recently revised in **2019-09-11 13:23:55**

* **原文**：[MDN - matchAll()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/matchAll)

* **功能**：`matchAll()` 方法返回一个包含所有匹配正则表达式及分组捕获结果的迭代器。

* **语法**：`str.matchAll(regexp)`
  * `regexp`：正则表达式对象。

* **返回值**：一个迭代器。

* **代码**：

```js
const regexp = RegExp('foo*','g'); 
const str = 'table football, foosball';
let matches = str.matchAll(regexp);

for (const match of matches) {
  console.log(match);
}
// Array [ "foo" ]
// Array [ "foo" ]
// 输出两次
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

