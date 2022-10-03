方法 - join()
===

> Create by **jsliang** on **2019-09-17 09:34:38**  
> Recently revised in **2019-09-17 09:34:47**

* **原文**：[MDN - join()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/join)

* **功能**：`join()` 方法将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串

* **语法**：`arr.join(separator)`
  * `separator` 是合并的形式。例如 `''` 就是不以任何形式拼接成字符串：`['hello', 'hi'].join('') -> 'hellohi'`；例如 `'-'` 就是以 `-` 形式拼接成字符串：`['hello', 'hi'].join('') -> 'hello-hi'`

* **返回值**：一个所有数组元素连接的字符串。

* **代码**：

```js
var a = ['Wind', 'Rain', 'Fire'];
var myVar1 = a.join();      // myVar1 的值变为 "Wind,Rain,Fire"
var myVar2 = a.join(', ');  // myVar2的值变为"Wind, Rain, Fire"
var myVar3 = a.join(' + '); // myVar3的值变为"Wind + Rain + Fire"
var myVar4 = a.join('');    // myVar4的值变为"WindRainFire"
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

