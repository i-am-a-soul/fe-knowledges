方法 - replace()
===

> Create by **jsliang** on **2019-09-11 13:24:45**  
> Recently revised in **2019-09-11 16:59:06**

* **原文**：[MDN - replace()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)

* **功能**：`replace()` 方法返回一个由替换值（`replacement`）替换一些或所有匹配的模式（`pattern`）后的新字符串。模式可以是一个字符串或者一个正则表达式，替换值可以是一个字符串或者一个每次匹配都要调用的回调函数。

* **语法**：`str.replace(regexp |substr, newSubStr| function)`
  * `regexp`：正则表达式。
  * `substr`：一个将被 `newSubStr` 替换的字符串。其被视为一整个字符串，而不是一个正则表达式。仅第一个匹配项会被替换。
  * `newSubStr`：用于替换掉第一个参数在原字符串中的匹配部分的字符串。该字符串中可以内插一些特殊的变量名。
  * `function`：一个用来创建新子字符串的函数，该函数的返回值将替换掉第一个参数匹配到的结果。

* **返回值**：一个部分或全部匹配由替代模式所取代的新的字符串。

* **代码**：

```js
var str = 'Twas the night before Xmas...';
var newstr = str.replace(/xmas/i, 'Christmas');
console.log(newstr);  // Twas the night before Christmas...
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

