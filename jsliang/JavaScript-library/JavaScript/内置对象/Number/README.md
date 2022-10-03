Number
===

> Create by **jsliang** on **2019-09-16 15:40:32**  
> Recently revised in **2019-09-18 08:51:07**

* **原文**：[MDN - Number](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number)

* **功能**：`Number` 可以将其他类型的值转为数字。

* **方法**：
  * `new Map()`：新建一个 `Map` 对象
  * `Number(x)`：将其他类型的值转为数字
  * `Number.MAX_SAFE_INTEGER`：JavaScript 中最大的安全整数 (2 的 53 次方 - 1)。
  * `Number.MIN_SAFE_INTEGER`：JavaScript 中最小的安全整数 (-(2 的 53 次方 - 1)).

* **代码**：

```js
Number("123")     // 123
Number("")        // 0
Number("0x11")    // 17
Number("0b11")    // 3
Number("0o11")    // 9
Number("foo")     // NaN
Number("100a")    // NaN
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

