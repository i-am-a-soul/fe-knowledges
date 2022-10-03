方法 - fromCharCode()
===

> Create by **jsliang** on **2019-09-18 10:42:21**  
> Recently revised in **2019-09-18 10:42:25**

* **原文**：[MDN - fromCharCode()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/fromCharCode)

* **功能**：静态 `String.fromCharCode()` 方法返回由指定的 UTF-16 代码单元序列创建的字符串。简单来说，就是接受一个 Unicode 值，然后返回一个字符串。例如 65 - A，66 - B

* **语法**：`fromCharCode(num)`
  * `num`：范围在 0-65535 之间，65 对应 A、66 对应 B，详情可以查看百度百科 [ASCII](https://baike.baidu.com/item/ASCII/309296?fr=aladdin)

* **返回值**：一个长度为 N 的字符串，由 N 个指定的 UTF-16 代码单元组成。

* **代码**：

```js
String.fromCharCode(65, 66, 67);  // 'ABC'
String.fromCharCode(0x2014)       // '—'
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

