Number - 数字化金额
===

> Create by **jsliang** on **2020-09-27 23:15:09**  
> Recently revised in **2020-09-27 23:24:58**

<!-- 目录开始 -->
## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- |
| [一 目录](#chapter-one) |
| [二 前言](#chapter-two) |
| [三 for 遍历](#chapter-three) |
| [四 API 方案一](#chapter-four) |
| [五 API 方案二](#chapter-five) |
| [六 正则](#chapter-six) |
<!-- 目录结束 -->

## 二 前言


  
将 `1234567890` 转为 `1,234,567,890`。

参考文献：

* [js，正则实现金钱格式化](https://blog.csdn.net/qq_36279445/article/details/78889305)

## 三 for 遍历


  
```js
const num = String(1234567890);
let result = '';

for (let i = num.length - 1; i >= 0; i--) {
  if (i !== num.length - 1 && i % 3 === 0) {
    result = num[i] + ',' + result;
  } else {
    result = num[i] + result;
  }
}

console.log(result);
```

## 四 API 方案一


  
```js
console.log(
  String(1234567890).split('').reverse().reduce((prev, next, index) => (index % 3) === 0 ? next + ',' + prev : next + prev)
);
```

## 五 API 方案二


  
```js
console.log(
  (1234567890).toLocaleString('en-US')
);
```

## 六 正则


  
```js
String(1234567890).replace(/\B(?=(\d{3})+(?!\d))/g, ',');
```

---

