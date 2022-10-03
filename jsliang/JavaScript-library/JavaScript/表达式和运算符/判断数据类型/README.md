判断数据类型
===

> Create by **jsliang** on **2019-10-16 00:42:32**  
> Recently revised in **2019-10-16 01:49:44**

本文将通过下方知识点，来讲解判断 JavaScript 数据类型的 4 种方法：

* `typeof()`
* `instanceof()`
* `constructor`
* `Object.prototype.toString.call()`

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 typeof](#chapter-three) |
| [四 instanceof](#chapter-four) |
| [五 constructor](#chapter-five) |
| [六 Object.prototype.toString.call()](#chapter-six) |
| [七 总结](#chapter-seven) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



不管是面试中，亦或在工作上，会出现这么个场景：

* **如何判断某个 JavaScript 字段的数据类型？**

当然，它还可能是某个知识点的附赠品，例如：

* **当你进行深拷贝数据的时候，你是如何判断这个字段是什么类型的？你知道判断数据类型有几种方式么？它们优缺点在哪？**

那么，本文来讲解下，判断 JavaScript 数据类型的四种方法！

## <a name="chapter-three" id="chapter-three">三 typeof</a>



```js
/**
 * @name typeof示例
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

如上，可以看出，通过 `typeof`，我们可以判断大多数的类型，但是，它存在缺陷：

1. 判断 `typeof null`，会得到 `object`；
2. 判断构造函数 `typeof new String('String')` 或者 `typeof new Number(123)` 等……，也会得到 `object`。

即通过 `typeof` 进行数据类型判断会有一定的问题。

> 详细研究可以看 **jsliang** 的学习文档[《判断数据类型 - typeof》](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%92%8C%E8%BF%90%E7%AE%97%E7%AC%A6/%E5%88%A4%E6%96%AD%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B/%E5%88%A4%E6%96%AD%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B-typeof.md)

## <a name="chapter-four" id="chapter-four">四 instanceof</a>



```js
/**
 * @name instanceof示例1
 * @description 检测字符串类型
 */
const simpleString = '这是简单的 String';
const newString = new String('这是 New 出来的 String');

console.log(simpleString instanceof String); // false，检查原型链会返回 undefined
console.log(newString instanceof String); // true

/**
 * @name instanceof示例2
 * @description 检测数字类型
 */
const simpleNumber = 123;
const newNumber = new Number(123);

console.log(simpleNumber instanceof Number); // false
console.log(newNumber instanceof Number); // true

/**
 * @name instanceof示例3
 * @description 检测对象类型
 */
const simpleOjbect = {};
const newObject = new Object();

console.log(simpleOjbect instanceof Object); // true
console.log(newObject instanceof Object); // true
```

如上，`instanceof` 可能表现的差强人意，虽然它是可以检测数据类型，但是对于 `'' instanceof String` 以及 `123 instanceof Number` 等会返回 `false`，不太满足我们需求。

其实 `instanceof` 主要用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链上，这块知识点到时候我们可以进一步进行学习探索。（一件值得期待的事）

> 详细研究可以看 **jsliang** 的学习文档[《判断数据类型 - instanceof》](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%92%8C%E8%BF%90%E7%AE%97%E7%AC%A6/%E5%88%A4%E6%96%AD%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B/%E5%88%A4%E6%96%AD%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B-instanceof.md)

## <a name="chapter-five" id="chapter-five">五 constructor</a>



```js
/**
 * @name constructor示例
 * @description constructor 检测对象类型
 */
const arr = [];
console.log(arr.constructor === Array); // true

const obj = {};
console.log(obj.constructor === Object); // true

const num = 1;
console.log(num.constructor === Number); // true

const str = '1';
console.log(str.constructor === String); // true

const bool = true;
console.log(bool.constructor === Boolean); // true

const nul = null;
// console.log(nul.constructor); // 报错：Uncaught TypeError: Cannot read property 'constructor' of null at <anonymous>:1:5

const undefin = undefined;
// console.log(undefin.constructor); // 报错：Uncaught TypeError: Cannot read property 'constructor' of null at <anonymous>:1:5
```

`constructor` 和前面的 `typeof`、`instanceof` 不同，`typeof` 和 `instanceof` 是属于 **表达式和运算符** 分类下的，而 `constructor` 是直接关系到内置对象 `Object` 下。

当然，这里我们讲的是校验数据类型，通过 `[].constructor === Array` 或者 `(1).constructor === Number` 会返回 `true`，符合我们的预期。

但是很遗憾的表示，当你使用 `null.constructor` 或者 `undefined.constructor` 它会毫不留情的给你报：`Uncaught TypeError: Cannot read property 'constructor' of null at <anonymous>:1:5`，所以我们也不能强行使用 `constructor` 来做深拷贝时候的判断数据类型。

> 详细研究可以看 **jsliang** 的学习文档[《判断数据类型 - constructor》](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%92%8C%E8%BF%90%E7%AE%97%E7%AC%A6/%E5%88%A4%E6%96%AD%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B/%E5%88%A4%E6%96%AD%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B-constructor.md)

## <a name="chapter-six" id="chapter-six">六 Object.prototype.toString.call()</a>



```js
/**
 * @name toString示例
 * @description toString 检测对象类型
 */
const toString = Object.prototype.toString;

console.log(toString.call(new Date));     // [object Date]
console.log(toString.call(new String));   // [object String]
console.log(toString.call(Math));         // [object Math]
console.log(toString.call('jsliang'));    // [object String]
console.log(toString.call(123));          // [object Number]
console.log(toString.call([]));           // [object Array]
console.log(toString.call({}));           // [object Object]
console.log(toString.call(undefined));    // [object Undefined]
console.log(toString.call(null));         // [object Null]
```

在前面三种心有余而力不足的情况下，`Object.prototype.toString.call()` 就显得稳定而实用了。

如果你看过 jQuery 源码，你会发现它的数据类型检测也是通过这个实现的（`jQuery.type(obj)`）。

在检测数据类型方面，你不管检测 `Object.prototype.toString.call('aaa')`、`Object.prototype.toString.call(null)` 亦或者 `Object.prototype.toString.call(undefined)` 都能得到你要的类型格式：`[object String]`、`[object Null]`、`[object Undefined]`。

> 详细研究可以看 **jsliang** 的学习文档[《判断数据类型 - toString》](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%92%8C%E8%BF%90%E7%AE%97%E7%AC%A6/%E5%88%A4%E6%96%AD%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B/%E5%88%A4%E6%96%AD%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B-toString.md)

## <a name="chapter-seven" id="chapter-seven">七 总结</a>



如上，通过对比，我们得出结论，在进行 JavaScript 数据类型判断的时候，推荐使用：

* `Object.prototype.toString.call()`

当然，写到这里，虽然我们的文章看起来可能简洁短小点，但是 **jsliang** 已经感觉讲出了这四种方法在判断数据类型上的优缺点。

同时，如果小伙伴有跟着链接走起，你会发现可以涉及更多的知识点，例如：

* `apply()`
* `bind()`
* `call()`
* `apply()、bind() 以及 call() 的区别`
* ……

不折腾的前端，和咸鱼有什么区别。

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

