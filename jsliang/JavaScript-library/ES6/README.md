ES6 小册
===

> Create by **jsliang** on **2020-4-12 20:54:38**  
> Recently revised in **2020-04-28 11:06:53**

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 let & var & const](#chapter-three) |
| [四 块级作用域](#chapter-four) |
| [五 解构赋值](#chapter-five) |
| [六 展开运算符](#chapter-six) |
| [七 Set](#chapter-seven) |
| [八 Map](#chapter-eight) |
| [九 新增函数拓展](#chapter-night) |
| [十 新增数组拓展](#chapter-ten) |
| [十一 新增字符串拓展](#chapter-eleven) |
| [十二 新增对象拓展](#chapter-twelve) |
| [十三 Babel](#chapter-thirteen) |
| [十四 ES6 高级 - 异步专题](#chapter-fourteen) |
| [十五 ES6 高级 - MVVM](#chapter-fifteen) |
| [十六 总结](#chapter-sixteen) |
| [十七 参考文献](#chapter-seventeen) |

## 二 前言



ECMAScript 2015，简称 ES6。

ECMAScript 是形成 JavaScript 语言基础的脚本语言。

它的历史版本为：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Language_Resources

在 2015 年 6 月，ECMAScript 2015（6th Edition）通过批准，是最新发布的规范文档。

这里推荐阮一峰的 ES6 入门教程：https://es6.ruanyifeng.com/

里面内容非常丰富，毕竟是出版过的书籍，非常推荐。

## 三 let & var & const



### 3.1 let



* 暂时性死区：只要块级作用域内存在 `let` 命令，它所声明的变量就绑定这个区域，不再受外部的影响。在代码块内，使用 `let` 声明变量之前，该变量都是不可用的，所以叫 “暂时性死区”。
* 不能重复声明
* 块级作用域
* `let` 不会被预解析
* 手册地址：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/let

### 3.2 const



* 常量不能重新赋值；数组、对象的值可被修改
* 暂时性死区：只要块级作用域内存在 `let` 命令，它所声明的变量就绑定这个区域，不再受外部的影响。在代码块内，使用 `let` 声明变量之前，该变量都是不可用的，所以叫 “暂时性死区”。
* 不能重复声明
* 块级作用域
* `const` 不会被预解析
* 手册地址：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/const

### 3.3 let 和 var 比较



* `var` 声明的变量只能是全局或者整个函数块的
* `let` 允许声明一个在作用域限制在块级的变量、语句或者表达式（块级作用域）
* `let` 不能重复声明
* `let` 存在临时死区（temporal dead zone）
* `let` 不会被预解析（hoisting）

### 3.4 let、var 和 const 比较



* `var`：

1. `var` 可以重复声明
2. 作用域：全局作用域 和 函数作用域
3. 会进行预解析

* `let`：

1. 统一作用域下不能重复声明
2. 作用域：全局作用域 和 块级作用域 `{}`
3. 不进行预解析

* `const`：

1. `let` 有的它也有
2. 初始化必须赋值
3. 赋值后不能改动类型

## 四 块级作用域



块语句用于组合零个或者多个语句，这个块由一对大括号 `{}` 界定。

而通过 `var` 声明的变量或者非严格模式下（non-strict mode）创建的函数声明没有块级作用域。

即：

```js
var x = 1;
{
console.log("🚀 ~ file: README.md ~ line 117 ~ | [十七 参考文献](#chapter-seventeen) |", | [十七 参考文献](#chapter-seventeen) |)
  var x = 2;
}
console.log(x); // 2
```

所以，如果我们希望能形成块级作用域，可以：

> ES5

```js
(function() {

})()
```

> ES6

```js
{
  var x = 1; // 或者 const x = 1;
}
```

* 参考文献：[【MDN】《block》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/block)

## 五 解构赋值



解构赋值语法是一种 Javascript 表达式。通过解构赋值，可以将属性/值从对象/数组中取出，赋值给其他变量。

* 对象的解构赋值
* 数组的解构赋值
* 字符串的解构赋值
* 手册地址：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment

```js
// 对象的解构赋值
const obj = {
  a: 1,
  b: 2,
};
const {objA, objB, objC} = obj;
console.log(objA, objB, objC); // 1 2 undefined

// 数组的解构赋值
let a = 0, b = 1;
// 数组：swap
const c = a;
a = b;
b = c;
console.log(a, b); // 1 0
// 数组：结构赋值
const [d, e] = [b, a];
console.log(d, e); // 0 1

// 字符串的解构赋值
const str = 'abc';
const [str1, str2] = str;
console.log(str1, str2); // a b

// 数字的解构赋值
const [a1, b1] = 123;
// 报错：VM208:1 Uncaught TypeError: 123 is not iterable
// MDN：为了统一集合类型，ES6 标准引入了新的 iterable 类型，Array、Map 和 Set 都属于 iterable 类型。
```

## 六 展开运算符



展开语法（Spread syntax），可以在函数调用/数组构造时, 将数组表达式或者 `string` 在语法层面展开；还可以在构造字面量对象时, 将对象表达式按 `key-value` 的方式展开。

* 对象展开
* 数组展开
* 手册地址：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax

```js
// 数组展开
const arr1 = [1, 2, 3];
const arr2 = ['a', 'b', ...arr1, 'c'];
console.log(arr2); // ['a', 'b', 1, 2, 3, 'c']

const [a, b, ...c] = arr;
console.log(a, b, c); // 'a', 'b', [1, 2, 3, 'c']


// 对象展开
const obj1 = {
  a: 1,
  b: 2,
};
const obj2 = {
  ...obj1,
  c: 3,
  d: 4,
};
console.log(obj2); // { a: 1, b: 2, c: 3, d: 4 }
```

## 七 Set



`Set` 对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用。

* `Set` 对象的数据结构
* `Set` 相关属性与方法
  * `size` 属性
  * `clear()`、`delete()`、`get()`、`has()`、`add()`
* 手册地址：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set

## 八 Map



`Map` 对象保存键值对，并且能够记住键的原始插入顺序。任何值(对象或者原始值) 都可以作为一个键或一个值。

* `Map` 对象的数据结构
* `Map` 相关属性与方法
* `size` 属性
* `clear()`、`delete()`、`get()`、`has()`、`set()`
* 手册地址：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map

## 九 新增函数拓展



箭头函数表达式的语法比函数表达式更简洁，并且没有自己的 `this`、`arguments`、`super` 或 `new.target`。

箭头函数表达式更适用于那些本来需要匿名函数的地方，并且它不能用作构造函数。

剩余参数语法（...arg）允许我们将一个不定数量的参数表示为一个数组。

* 箭头函数
  * 箭头函数的各种写法
  * 箭头函数的 `this` 问题
  * 箭头函数的不定参问题
  * 手册地址：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions
* `rest` 参数（剩余参数）设置：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Rest_parameters
* 参数默认值设置

> 代码 1：普通函数、箭头函数 以及 不定参

```js
// 普通函数
function fn1() {
  return ;
};

// 箭头函数
const fn2 = () => {
  return ;
};

const getSum = num => num *2;
console.log(getSum(10)); // 20

// 不定参 - rest 参数
const fn3 = (a, b, ...arg) => {
  console.log(a, b, arg);
};
fn3(1, 2, 3, 4); // 1 2 [3, 4]
```

> 代码 2：this 指向问题

```js
// this 指向问题
document.onclick = function() {
  console.log(this); // #document
};
document.onclick = () => {
  console.log(this); // Window
}
// 箭头函数本身没有 this，调用箭头函数的 this 时，指向是其声明时所在的作用域的 this。
```

> 代码 3：this 题目

```js
let fn;
let fn2 = function() {
  console.log(this);
  fn = () => {
    console.log(this);
  };
};
fn2(); // Window
fn(); // Window

fn2 = fn2.bind(document.body);
fn2(); // body
fn(); // body
```

> 代码 4：参数默认值

```js
const fn = (a = 10, b = 2) => {
  console.log(a * b); // 20
};
fn();
```

## 十 新增数组拓展


ES6 新增了一些数组拓展：

* `Array.from()`、`Array.of()`
* `find()`、`findIndex()`、`includes()`
* `flat()`、`flatMap()`
* `fill()`
* 手册地址：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array

将类数组转成数组：

> 代码 1：Array.from()

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
    </ul>

    <script>
      let liItems = document.querySelectorAll("ul li");
      let arr1 = [];
      const li1 = Array.from(
        liItems,
        function (item, index) {
          console.log(item, index, this);
          return index;
        },
        arr1
      );
      /*
        * <li>1</li> 0 []
        * <li>2</li> 1 []
        * <li>3</li> 2 []
        * <li>4</li> 3 []
      */
      console.log(li1); // [0, 1, 2, 3]

      const arr2 = [...liItems];
      console.log(arr2); // [li, li, li, li]
    </script>
  </body>
</html>
```

> 代码 2：Array.of()

```js
console.log(Array.of(1, 2, 3, 4, 'A')); // [1, 2, 3, 4, "A"]
```

> 代码 3：Array.isArray()

```js
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
    </ul>

    <script>
      let liItems = document.querySelectorAll("ul li");
      console.log(Array.isArray(liItems)); // false
      console.log(Array.isArray([1, 2, 3, 4])); // true
    </script>
  </body>
</html>
```

其他的不一一例举，可自行查看 MDN 文档。

## 十一 新增字符串拓展



ES6 新增了一些字符串扩展：

* `includes()`、`startsWith()`、`endsWith()`
* `repeat()`
* 模板字符串
* 手册地址：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String

## 十二 新增对象拓展



ES6 新增了一些对象拓展：

* 属性简洁表示法
* 属性名表达式
* `Object.assign()`
* `Object.is`
* 手册地址：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object

> 代码 1：简洁表示法

```js
const a = 0, b = 1;
let obj1 = {
  a: a,
  b: b,
};
console.log(obj1); // {a: 0, b: 1}
let obj2 = {
  a,
  b,
};
console.log(obj2); // {a: 0, b: 1}
```

> 代码 2：属性名表达式

```js
const name = '小明';
const obj = {
  c() {
    console.log('a');
  },
  [name]: 18,
};
console.log(obj); // {c: ƒ, 小明: 18}
```

> 代码 3：Object.assign() 浅拷贝

```js
const obj1 = {
  a: 1,
  b: 2,
};
const obj2 = {
  c: 3,
  d: 4,
};
console.log(Object.assign({}, obj1, obj2)); // {a: 1, b: 2, c: 3, d: 4}
```

> 代码 4：Object.is 判断

```js
// 大致和三目运算符一致，但是有区别
console.log(+0 === -0);           // true
console.log(Object.is(+0, -0));   // false
console.log(NaN === NaN);         // false
console.log(Object.is(NaN, NaN)); // true
```

## 十三 Babel



Babel 是一个 JavaScript 编译器。

* 手册地址：https://www.babeljs.cn/
* Babel 基本使用方法

> https://unpkg.com/@babel/standalone/babel.min.js

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>babel</title>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script>
      "use strict";

      function ownKeys(object, enumerableOnly) {
        var keys = Object.keys(object);
        if (Object.getOwnPropertySymbols) {
          var symbols = Object.getOwnPropertySymbols(object);
          if (enumerableOnly)
            symbols = symbols.filter(function (sym) {
              return Object.getOwnPropertyDescriptor(object, sym).enumerable;
            });
          keys.push.apply(keys, symbols);
        }
        return keys;
      }

      function _objectSpread(target) {
        for (var i = 1; i < arguments.length; i++) {
          var source = arguments[i] != null ? arguments[i] : {};
          if (i % 2) {
            ownKeys(Object(source), true).forEach(function (key) {
              _defineProperty(target, key, source[key]);
            });
          } else if (Object.getOwnPropertyDescriptors) {
            Object.defineProperties(
              target,
              Object.getOwnPropertyDescriptors(source)
            );
          } else {
            ownKeys(Object(source)).forEach(function (key) {
              Object.defineProperty(
                target,
                key,
                Object.getOwnPropertyDescriptor(source, key)
              );
            });
          }
        }
        return target;
      }

      function _defineProperty(obj, key, value) {
        if (key in obj) {
          Object.defineProperty(obj, key, {
            value: value,
            enumerable: true,
            configurable: true,
            writable: true,
          });
        } else {
          obj[key] = value;
        }
        return obj;
      }

      var obj1 = {
        b: 2,
        c: 3,
      };

      var obj2 = _objectSpread(
        {
          a: 1,
        },
        obj1,
        {
          d: 4,
        }
      );

      console.log(obj2); // {a: 1, b: 2, c: 3, d: 4}
      //# sourceMappingURL=data:application/json;charset=utf-8;base64,eyJ2ZXJzaW9uIjozLCJzb3VyY2VzIjpbIklubGluZSBCYWJlbCBzY3JpcHQiXSwibmFtZXMiOlsib2JqMSIsImIiLCJjIiwib2JqMiIsImEiLCJkIiwiY29uc29sZSIsImxvZyJdLCJtYXBwaW5ncyI6Ijs7Ozs7Ozs7QUFDSSxJQUFNQSxJQUFJLEdBQUc7QUFDWEMsRUFBQUEsQ0FBQyxFQUFFLENBRFE7QUFFWEMsRUFBQUEsQ0FBQyxFQUFFO0FBRlEsQ0FBYjs7QUFJQSxJQUFNQyxJQUFJO0FBQ1JDLEVBQUFBLENBQUMsRUFBRTtBQURLLEdBRUxKLElBRks7QUFHUkssRUFBQUEsQ0FBQyxFQUFFO0FBSEssRUFBVjs7QUFLQUMsT0FBTyxDQUFDQyxHQUFSLENBQVlKLElBQVosRSxDQUFtQiIsInNvdXJjZXNDb250ZW50IjpbIlxuICAgIGNvbnN0IG9iajEgPSB7XG4gICAgICBiOiAyLFxuICAgICAgYzogMyxcbiAgICB9O1xuICAgIGNvbnN0IG9iajIgPSB7XG4gICAgICBhOiAxLFxuICAgICAgLi4ub2JqMSxcbiAgICAgIGQ6IDQsXG4gICAgfTtcbiAgICBjb25zb2xlLmxvZyhvYmoyKTsgLy8ge2E6IDEsIGI6IDIsIGM6IDMsIGQ6IDR9XG4gICJdfQ==
    </script>
  </head>
  <body>
    <script type="text/babel">
      const obj1 = {
        b: 2,
        c: 3,
      };
      const obj2 = {
        a: 1,
        ...obj1,
        d: 4,
      };
      console.log(obj2); // {a: 1, b: 2, c: 3, d: 4}
    </script>
  </body>
</html>
```

## 十四 ES6 高级 - 异步专题



### 14.1 ES6 同步和异步


  
同步和异步是一种消息通知机制：

* 同步阻塞:

A 调用 B，B 处理获得结果，才返回给 A。

A 在这个过程中，一直等待 B 的处理结果，没有拿到结果之前，需要 A（调用者）一直等待和确认调用结果是否返回，拿到结果，然后继续往下执行。

做一件事，没有拿到结果之前，就一直在这等着，一直等到有结果了，再去做下边的事

* 异步非阻塞:

A 调用 B，无需等待 B 的结果，B 通过状态，通知等来通知 A 或回调函数来处理。

做一件事，不用等待事情的结果，然后就去忙别的了，有了结果，再通过状态来告诉我，或者通过回调函数来处理。

### 14.2 回调运动框架 



代码在仓库第 《006-方块运动-回调（callback）》 文件夹：https://github.com/LiangJunrong/all-for-one

### 14.3 Promise



代码在仓库第 《007-方块运动-链式（Promise）》 文件夹：https://github.com/LiangJunrong/all-for-one 

`Promise` 的三种状态：

* `pedding`
* `resolved`
* `reject`

```js
const p1 = new Promise((resolve, reject) => {});
console.log(p1); // Promise {<pending>}

const p2 = new Promise((resolve, reject) => {
  resolve('解决了！');
});
console.log(p2); // Promise {<resolved>: "解决了！"}

const p3 = new Promise((resolve, reject) => {
  reject('失败了！');
});
console.log(p3); // Promise {<rejected>: "失败了！"}
// 报错：Uncaught (in promise) 失败了！
```

> resolve & reject

```js
const p1 = Promise.resolve('成功');
console.log(p1); // Promise {<resolved>: "成功"}

const p2 = Promise.reject('失败');
console.log(p2); // Promise {<rejected>: "失败"}
```

* `then`：`Promise` 对象会有 `then` 方法，它传递两个参数：`onresolve` 和 `onreject`。

```js
const p1 = new Promise((resolve, reject) => {
  resolve({ name: 'jsiang', age: '25' });
}).then((res) => {
  console.log('调用成功：', res);
}, (error) => {
  console.log('调用失败：', error);
});
// 调用成功： {name: "jsiang", age: "25"}

const p2 = new Promise((resolve, reject) => {
  reject({ code: '999', message: '接口报错' });
}).then((res) => {
  console.log('调用成功：', res);
}, (error) => {
  console.log('调用失败：', error);
})
// 调用失败： {code: "999", message: "接口报错"}
```

* `then` 有三种返还值

```js
const p = new Promise((resolve, reject) => {
  resolve('调用成功1');
});

// 1. then 里面没有返回 -> 默认返回一个 Promise
const res1 = p.then((res) => {

});
console.log(res1);
/*
__proto__: Promise
[[PromiseStatus]]: "resolved"
[[PromiseValue]]: undefined
*/

// 2. then 里面有返回 -> 将它的值塞到 Promise 中
const res2 = p.then((res) => {
  return 'Hello jsliang';
});
console.log(res2);
/*
__proto__: Promise
[[PromiseStatus]]: "resolved"
[[PromiseValue]]: "Hello jsliang"
*/

// 3. then 里面返回一个新的 Promise
const res3 = p.then((res) => {
  return new Promise((resolve, reject) => {
    resolve('调用成功2');
  })
});
console.log(res3);
/*
__proto__: Promise
[[PromiseStatus]]: "resolved"
[[PromiseValue]]: "调用成功2"
*/
```

* `catch`：将所有异常丢到同一块地方

```js
const p = new Promise((resolve, reject) => {
  reject('调用失败');
}).then((res) => {
  console.log(res);
}).catch((err) => {
  console.log('catch 异常：', err);
})
// catch 异常： 调用失败
```

> `Promise` 方法改造加载图片

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <script>
    const getImage = () => {
      return new Promise((resolve, reject) => {
        const img = new Image();
        img.src = 'https://jsliang.com';
        img.onload = () => {
          document.querySelector('body').appendChild(img);
          resolve('图片加载完毕');
        };
        img.onerror = () => {
          reject('图片加载失败');
        }
      });
    };
    getImage().then((res) => {
      console.log(res);
    }).catch((error) => {
      console.log(error); // 图片加载失败
    });
  </script>
</body>
</html>
```

* `all`：所有内容成功则成功

```js
const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log();
    resolve('p1 执行完毕');
  }, 1000);
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('p2 执行完毕');
    // reject('p2 执行完毕');
  }, 3000);
});
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('p3 执行完毕');
  }, 2000);
});
Promise.all([p1, p2, p3]).then(res => {
  console.log(res); // ["p1 执行完毕", "p2 执行完毕", "p3 执行完毕"]
}).catch(err => {
  console.log(err);
});
```

* `race`：执行最快的结果

```js
const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('p1 执行完毕');
  }, 1000);
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('p2 执行完毕');
    // reject('p2 执行完毕');
  }, 3000);
});
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('p3 执行完毕');
  }, 2000);
});
Promise.race([p1, p2, p3]).then(res => {
  console.log(res); // p1 执行完毕
}).catch(err => {
  console.log(err);
});
```

### 14.4 async 和 await



代码在仓库第 《008-方块运动-等待（async...await））》 文件夹：https://github.com/LiangJunrong/all-for-one 

`async` 和 `await` 是一起出现的，基于 `Promise`。

`await` 后面一定要 `Promise` 对象。

```js
const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('p1 执行完毕');
    resolve({ code: '0', name: 'jsliang', age: 25 });
  }, 1000);
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('p2 执行完毕');
    resolve({ code: '999', error: '后端接口报错' });
    // reject('未知错误');
  }, 3000);
});
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('p3 执行完毕');
    resolve({ code: '0', like: 'play' });
  }, 2000);
});
async function fn() {
  try {
    const res1 = await p1;
    const res2 = await p3;
    const res3 = await p2;
    if (res1.code === '0' && res2.code === '0' && res3.code === '0') {
      console.log(res1);
      console.log(res2);
      console.log(res3);
    } else {
      console.log(`报错：${res1.error || res2.error || res3.error}`);
    }
  } catch (err) {
    console.log(err);
  }
};
fn();
/*
p1 执行完毕
p3 执行完毕
p2 执行完毕
报错：后端接口报错
*/
```

## 十五 ES6 高级 - MVVM



代码实现在：https://github.com/LiangJunrong/all-for-one

* 《009-双向数据绑定-模板语法》
* 《010-双向数据绑定-模板语法（优化正则）》
* 《011-双向数据绑定-简单实现（Object.defineProperty）》
* 《012-双向数据绑定-发布订阅者模式》
* 《013-双向数据绑定-改造升级（Proxy）》
* 《014-双向数据绑定-输入框绑定（v-modal）》
* 《015-双向数据绑定-HTML替换（v-html）》

在实现的过程中，思考了下东西。

原生 JavaScript 实现 Vue 中的 `{{ message }}` 需要考虑的内容：

1. 先区分文本节点还是标签节点。`{{ message }}` 或者 `<span>{{ message }}</span>` 或者其他。
2. 如果是单个文本，即文本内仅有一个 `{{ message }}`，那么我们可以正则匹配然后将其替换为传入的数据。
3. 如果是多个文本，即文本为 `{{ message }} - {{ name }}` 之类的格式，那么我们可以在上面条件的基础上，通过正则的 `match()` 方法匹配所有，然后逐个替换。
4. 如果是标签节点，即 `<div>{{ message }}</div>`（有可能里面还有更多嵌套），我们就需要考虑递归实现。

> 问题：

1. 在课程中，用的是正则实现，可以用 “人” 能理解的方式写么？
2. 在课程中，用的是递归实现，那么它必定有所局限，谈谈局限在哪，怎么解决？（微信小程序之前有个规则：不能渲染超过 5 层的）
3. 观察者模式和发布订阅模式的区别？发布订阅模式比观察者模式解耦性更强。
4. `defineProperty` 和 `Proxy` 区别。

## 十六 总结



如上，即为 **jsliang** 整理的 ES6 小册，但是是不完整版的，还差：

1. `iterable`
2. `module`

这些需要补充的点，后面会逐个添加进来。

* `iterable`：

ES6 为字符串添加了遍历器接口，使得字符串可以被 `for...of` 循环遍历

* 模板字符串：

```js
let arr1 = '', arr2 = '';
let name = 'jsliang';
arr1 += 'Hello, my name is: ' + name;
arr2 += `Hello, my name is ${name}`;
```

1. 模板字符串支持多行
2. 模板字符串支持 `${}` 内存放变量，运算以及函数

## 十七 参考文献



* [【MDN】《ECMAScript 历史》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Language_Resources)
* [【MDN】《let》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/let)
* [【MDN】《const》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/const)
* [【MDN】《block》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/block)
* [【MDN】《解构赋值》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
* [【MDN】《展开语法》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
* [【MDN】《Set》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set)
* [【MDN】《Map》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map)
* [【MDN】《箭头函数》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
* [【MDN】《剩余参数》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Rest_parameters)
* [【MDN】《Array》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)
* [【MDN】《String》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)
* [【MDN】《Object》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)
* [【Babel 中文网】](https://www.babeljs.cn/)

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

