693 - 交替位二进制数（binary-number-with-alternating-bits）
===

> Create by **jsliang** on **2019-12-16 08:40:58**  
> Recently revised in **2019-12-16 09:07:45**

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题及测试](#chapter-three) |
| [四 LeetCode Submit](#chapter-four) |
| [五 解题思路](#chapter-five) |

## 二 前言



* **难度**：简单
* **涉及知识**：位运算
* **题目地址**：https://leetcode-cn.com/problems/binary-number-with-alternating-bits/
* **题目内容**：

```
给定一个正整数，检查他是否为交替位二进制数：
换句话说，就是他的二进制数相邻的两个位数永不相等。

示例 1:

输入: 5
输出: True
解释:
5 的二进制数是: 101

示例 2:
输入: 7
输出: False
解释:
7 的二进制数是: 111

示例 3:
输入: 11
输出: False
解释:
11 的二进制数是: 1011

示例 4:
输入: 10
输出: True
解释:
10 的二进制数是: 1010
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} n
 * @return {boolean}
 */
var hasAlternatingBits = function(n) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 交替位二进制数
 * @param {number} n
 * @return {boolean}
 */
const hasAlternatingBits = (n) => {
  const newNumber = n.toString(2);
  for (let i = 0; i < newNumber.length - 1; i++) {
    if (newNumber[i] === newNumber[i + 1]) {
      return false;
    }
  }
  return true;
};

console.log(hasAlternatingBits(5)); // true
console.log(hasAlternatingBits(7)); // false
console.log(hasAlternatingBits(11)); // false
console.log(hasAlternatingBits(10)); // true
```

`node index.js` 返回：

```js
true
false
false
true
```

## 四 LeetCode Submit



```js
Accepted
* 204/204 cases passed (76 ms)
* Your runtime beats 23.81 % of javascript submissions
* Your memory usage beats 45 % of javascript submissions (33.7 MB)
```

## 五 解题思路



**幸福来得太突然，解题来得太简单**。

上手直接代码：

> 使用 JavaScript 附带方法

```js
const hasAlternatingBits = (n) => {
  const newNumber = n.toString(2);
  for (let i = 0; i < newNumber.length - 1; i++) {
    if (newNumber[i] === newNumber[i + 1]) {
      return false;
    }
  }
  return true;
};
```

还没细细品味告诉我已经完毕了：

1. 通过 `toString(2)` 直接转二进制。
2. 遍历 `newNumber`，比较当前数字和下一个数字是否一致。

```js
Accepted
* 204/204 cases passed (76 ms)
* Your runtime beats 23.81 % of javascript submissions
* Your memory usage beats 45 % of javascript submissions (33.7 MB)
```

这时候，应该会有小伙伴吐槽：

* 用 JavaScript 附带的二进制转换算什么，有本事自己写啊~

明确的回复是：能用工具的人工作效率明显会比不用工具的人快。

但是总不能一棒子打死嘛，那就表演下真正的技术吧：

> 手写一个原生方法

```js
/**
 * @name 转二进制
 * @param {Number} number 需要转换的数字
 */
const binaryConversion = (number) => {
  let result = '';
  while (number > 0) {
    result += number % 2;
    number = Math.floor(number / 2);
  }
  return result;
};

/**
 * @name 交替位二进制数
 * @param {number} n
 * @return {boolean}
 */
const hasAlternatingBits = (n) => {
  const newNumber = binaryConversion(n);
  for (let i = 0; i < newNumber.length - 1; i++) {
    if (newNumber[i] === newNumber[i + 1]) {
      return false;
    }
  }
  return true;
};

console.log(hasAlternatingBits(5)); // true
console.log(hasAlternatingBits(7)); // false
console.log(hasAlternatingBits(11)); // false
console.log(hasAlternatingBits(10)); // true
```

Submit 提交：

```js
Accepted
* 204/204 cases passed (52 ms)
* Your runtime beats 99.21 % of javascript submissions
* Your memory usage beats 15 % of javascript submissions (34.2 MB)
```

搞定~

收工！

如果你有更好的思路或者观点，欢迎评论留言或者私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

