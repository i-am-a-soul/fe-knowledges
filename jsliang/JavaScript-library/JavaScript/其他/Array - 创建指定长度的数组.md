创建指定长度的数组
===

> Create by **jsliang** on **2020-01-27 18:02:59**  
> Recently revised in **2020-01-27 18:09:37**

创建指定长度的数组的几种方式：

> ... 扩展

```js
const arr1 = [...Array(3)].map((value, index) => index);
console.log(arr1);
// [0, 1, 2]
```

> Array.from

```js
const arr2 = Array.from(Array(3), (value, index) => index);
console.log(arr2);
// [0, 1, 2]
```

> 愚蠢法子

```js
const arr3 = [];
for (let i = 0; i < 3; i++) {
  arr3.push(i);
}
console.log(arr3);
// [0, 1, 2]
```

三种够用就行

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)


