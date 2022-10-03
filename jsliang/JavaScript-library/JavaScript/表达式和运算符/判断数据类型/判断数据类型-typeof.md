判断数据类型 - typeof
===

> Create by **jsliang** on **2019-10-15 16:33:27**  
> Recently revised in **2019-10-15 19:50:09**

* **原文**：[MDN - typeof](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof)

* **功能**：`typeof` 操作符返回一个字符串，表示未经计算的操作数的类型。

* **方法**：`typeof operand` 或者 `typeof(operand)`
  * `operand`：一个表示对象或原始值的表达式，其类型将被返回。

* **说明**：

下面列举下 `typeof` 可能的返回值：

| 类型 | 结果 |
| --- | --- |
| Undefined | 'undefined' |
| Null | 'object' |
| Boolean | 'boolead' |
| Number | 'number' |
| BigInt | 'bigint' |
| String | 'string' |
| Symbol | 'symbol' |
| Function | 'function' |
| 其他任何对象 | 'object' |

* **代码**：

```js
/**
 * @name typeof测试
 * @description 通过 typeof 检测各个数据类型的返回
 */
const test = {
  testUndefined: undefined,
  testNull: null,
  testBoolean: true,
  testNumber: 123,
  testBigInt: BigInt(1234), // 大于 2 的 53 次方算 BigInt
  testString: '123',
  testSymbol: Symbol(),
  testFunction: function() {
    console.log('function');
  },
  testObject: {
    obj: 'yes',
  },
  testObjectString: new String('String'),
  testObjectNumber: new Number(123),
}

console.log(typeof(test.testUndefined)); // undefined
console.log(typeof(test.testNull));      // object
console.log(typeof(test.testBoolean));   // boolean
console.log(typeof(test.testNumber));    // number
console.log(typeof(test.testBigInt));    // bigint
console.log(typeof(test.testString));    // string
console.log(typeof(test.testSymbol));    // symbol
console.log(typeof(test.testFunction));  // function
console.log(typeof(test.testObject));    // object
console.log(typeof(test.testObjectString));    // object
console.log(typeof(test.testObjectNumber));    // object
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

