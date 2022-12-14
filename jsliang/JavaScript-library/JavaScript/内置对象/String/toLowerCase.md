方法 - toLowerCase()
===

> Create by **jsliang** on **2019-09-16 14:36:42**  
> Recently revised in **2019-09-16 14:36:45**

* **原文**：[MDN - toLowerCase()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase)

* **功能**：`toLowerCase()` 会将调用该方法的字符串值转为小写形式，并返回。

* **语法**：`str.toLowerCase()`

* **返回值**：一个新的字符串，表示串转换为小写的调用字符。

* **代码**：

```js
console.log('中文简体 zh-CN || zh-Hans'.toLowerCase());
// 中文简体 zh-cn || zh-hans

​console.log( "ALPHABET".toLowerCase() ); 
// "alphabet"
```

* **注释**：`toLocalLowerCase` 区别于 `toLowerCase` 在于一些小种语言需要使用特定的 `toLocalLowerCase`/`toLocaleUpperCase` 进行转换大小写。

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

