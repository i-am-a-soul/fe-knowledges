231 - 2的幂（power-of-two）
===

> Create by **jsliang** on **2019-07-15 15:41:43**  
> Recently revised in **2019-09-18 13:45:28**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| &emsp;[3.1 解法 - 暴力破解](#chapter-three-one) |
| &emsp;[3.2 解法 - 无脑梭哈](#chapter-three-two) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：位运算、数学
* **题目地址**：https://leetcode-cn.com/problems/power-of-two/
* **题目内容**：

```
给定一个整数，编写一个函数来判断它是否是 2 的幂次方。

示例 1:
输入: 1
输出: true
解释: 20 = 1

示例 2:
输入: 16
输出: true
解释: 24 = 16

示例 3:
输入: 218
输出: false
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

### <a name="chapter-three-one" id="chapter-three-one">3.1 解法 - 暴力破解</a>



* **解题代码**：

```js
var isPowerOfTwo = function(n) {
  if (n === 1 || n === 2) {
    return true;
  }
  while (n > 2) {
    n = n / 2;
    if (n === 2) {
      return true;
    }
  }
  return false;
};
```

* **执行测试**：

1. `n`：`16`
2. `return`：`true`

* **LeetCode Submit**：

```js
✔ Accepted
  ✔ 1108/1108 cases passed (84 ms)
  ✔ Your runtime beats 99.6 % of javascript submissions
  ✔ Your memory usage beats 23.18 % of javascript submissions (35.5 MB)
```

* **解题思路**：

将这个数一直除于 2，当它的值接近 2 时，它有两种可能：

1. 等于 2，即这个数它刚好是 2 的幂。
2. 小于 2，即这个数不是 2 的幂。

最后，直接判断返回即可。

> 简单到 **jsliang** 无力吐槽

### <a name="chapter-three-two" id="chapter-three-two">3.2 解法 - 无脑梭哈</a>



* **解题代码**：

```js
var isPowerOfTwo = function(n) {
  return Number.isInteger(Math.log2(n));
};
```

* **执行测试**：

1. `n`：`16`
2. `return`：`true`

* **LeetCode Submit**：

```js
✔ Accepted
  ✔ 1108/1108 cases passed (96 ms)
  ✔ Your runtime beats 91.7 % of javascript submissions
  ✔ Your memory usage beats 12.28 % of javascript submissions (35.7 MB)
```

* **知识点**：

1. `Number`：将其他值转成数字值。[`Number` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Number/README.md)
2. `Math`：JS 中的内置对象，具有数学常数和函数的属性和方法。[`Math` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Math/README.md)

* **解题思路**：

通过 `Number` 来判断进行求底运算后的数字，是否为整数，如果是，则 `n` 是 2 的幂，如果不是，则返回 `false`。

> **jsliang** 更加无力吐槽了

* **进一步拓展**：

这道题还可以通过二进制进行位运算，不过 **jsliang** 兴致缺缺，小伙伴们可以进行尝试~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

