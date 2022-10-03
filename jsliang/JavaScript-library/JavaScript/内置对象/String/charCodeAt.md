方法 - charCodeAt()
===

> Create by **jsliang** on **2019-07-06 14:59:28**  
> Recently revised in **2019-09-10 17:24:23**

* **原文**：[MDN - charCodeAt()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt)

* **功能**：静态 `String.charCodeAt()` 方法返回 0 到 65535 之间的整数，表示给定索引处的 UTF-16 代码单元 (在 Unicode 编码单元表示一个单一的 UTF-16 编码单元的情况下，UTF-16 编码单元匹配 Unicode 编码单元。

* **语法**：`charCodeAt(index)`
  * `index`：一个大于等于 0，小于字符串长度的整数。如果不是一个数值，则默认为 0。详情可以查看百度百科 [ASCII](https://baike.baidu.com/item/ASCII/309296?fr=aladdin)

* **返回值**：返回值是一表示给定索引处（String 中 index 索引处）字符的 UTF-16 代码单元值的数字；如果索引超出范围，则返回 NaN。

* **代码**：

```js
'ABC'.charCodeAt(0) // 65
'ABC'.charCodeAt(1) // 66
'ABC'.charCodeAt(2) // 67
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

