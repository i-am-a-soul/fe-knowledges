方法 - push()
===

> Create by **jsliang** on **2019-09-17 09:23:32**  
> Recently revised in **2019-09-17 09:23:35**

* **原文**：[MDN - push()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push)

* **功能**：`push()` 方法将一个或多个元素添加到数组的末尾，并返回该数组的新长度。

* **语法**：`arr.push(element)`
  * `element`：需要传入到数组的元素

* **返回值**：当调用该方法时，新的 length 属性值将被返回。

* **代码**：

```js
let arr = [];
arr.push(1);
arr.push('2');
arr.push([3, 4, 5]);
arr.push([...6, 7, 8]);
console.log(arr);

/*
[1, "2", Array(3), 6, 7, 8]
0: 1
1: "2"
2: (3) [3, 4, 5]
3: 6
4: 7
5: 8
length: 6
*/
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

