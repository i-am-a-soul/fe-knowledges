方法 - pop()
===

> Create by **jsliang** on **2019-09-17 09:31:29**  
> Recently revised in **2019-09-17 09:31:32**

* **原文**：[MDN - pop()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)

* **功能**：`pop()` 方法从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。

* **语法**：
  * `arr.pop()`：返回从数组中删除的元素

* **返回值**：一个新数组，每个元素都是回调函数的结果。

* **代码**：

```js
let arr = [1, 2, 3, 4];
for(let i = 0, time = 1; i < arr.length; time++) {
  console.log(`------\n第 ${time} 次遍历：`);
  console.log(arr.pop());
  console.log(arr);
}

/* Console：
------
第 1 次遍历：
4
[ 1, 2, 3 ]
------
第 2 次遍历：
3
[ 1, 2 ]
------
第 3 次遍历：
2
[ 1 ]
------
第 4 次遍历：
1
[]
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

