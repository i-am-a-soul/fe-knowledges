方法 - slice()
===

> Create by **jsliang** on **2019-09-16 11:44:50**  
> Recently revised in **2019-09-16 11:46:29**

* **原文**：[MDN - slice()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/slice)

* **功能**：`slice()` 方法提取某个字符串的一部分，并返回一个新的字符串，且不会改动原字符串。

* **语法**：`str.slice(beginIndex, endIndex)`
  * `beginIndex`：从该索引（以 0 为基数）处开始提取原字符串中的字符。
  * `endIndex`：可选。在该索引（以 0 为基数）处结束提取字符串。如果省略该参数，`slice()` 会一直提取到字符串末尾。

* **返回值**：返回一个从原字符串中提取出来的新字符串。

* **代码**：

```js
var str1 = 'The morning is upon us.', // str1 的长度 length 是 23。
    str2 = str1.slice(1, 8),
    str3 = str1.slice(4, -2),
    str4 = str1.slice(12),
    str5 = str1.slice(30);
console.log(str2); // 输出：he morn
console.log(str3); // 输出：morning is upon u
console.log(str4); // 输出：is upon us.
console.log(str5); // 输出：''
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

