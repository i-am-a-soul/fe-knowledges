方法 - padStart()
===

> Create by **jsliang** on **2019-09-16 11:32:20**  
> Recently revised in **2019-09-16 11:36:26**

* **原文**：[MDN - padStart()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/padStart)

* **功能**：`padStart()` 方法用另一个字符串填充当前字符串(重复，如果需要的话)，以便产生的字符串达到给定的长度。填充从当前字符串的开始(左侧)应用的。

* **语法**：`str.padStart(targetLength, padString)`
  * `targetLength`：当前字符串需要填充到的目标长度。如果这个数值小于当前字符串的长度，则返回当前字符串本身。
  * `padString`：填充字符串。如果字符串太长，使填充后的字符串长度超过了目标长度，则只保留最左侧的部分，其他部分会被截断。

* **返回值**：在原字符串开头填充指定的填充字符串直到目标长度所形成的新字符串。

* **代码**：

```js
'jsliang'.padStart(10); // '   jsliang' 共 10 长度
'jsliang'.padStart(10, 'a'); // 'aaajsliang'
'jsliang'.padStart(20, 'JavaScriptLiang'); // JavaScriptLiajsliang
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

