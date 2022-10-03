009 - 回文数（palindrome-number）
===

> Create by **jsliang** on **2019-05-22 19:30:42**  
> Recently revised in **2019-09-18 09:30:54**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| &emsp;[3.1 解题 - 数组操作](#chapter-three-one) |
| &emsp;[3.1 解题 - 数学算法](#chapter-three-two) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：数学
* **题目地址**：https://leetcode-cn.com/problems/palindrome-number/
* **题目内容**：

```
判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

示例 1:
输入: 121
输出: true

示例 2:
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。

示例 3:
输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。

进阶:
你能不将整数转为字符串来解决这个问题吗？
```

## <a name="chapter-three" id="chapter-threed">三 解题</a>



* **官方题解**：https://leetcode-cn.com/problems/palindrome-number/solution/hui-wen-shu-by-leetcode/

解题千千万，官方独一家，上面是官方使用 C# 进行的题解。

小伙伴可以先自己在本地尝试解题，再看看官方解题，最后再回来看看 **jsliang** 讲解下使用 JavaScript 的解题思路。

### <a name="chapter-three-one" id="chapter-three-one">3.1 解法 - 数组操作</a>



* **解题代码**：

```js
var isPalindrome = function(x) {
  const arr = String(x).split('');
  for (let i = 0; i < arr.length / 2; i++) {
    if (arr[i] !== arr[arr.length - (i + 1)]) {
      return false;
    }
  }
  return true;
};
```

* **执行测试**：

1. `x`：`1231`
2. `return`：

```js
false
```

* **LeetCode Submit**：

```js
✔ Accepted
  ✔ 11509/11509 cases passed (316 ms)
  ✔ Your runtime beats 97.12 % of javascript submissions
  ✔ Your memory usage beats 67.78 % of javascript submissions (45.5 MB)
```

* **知识点**：

1. `split()`：`split()` 方法使用指定的分隔符字符串将一个 String 对象分割成字符串数组，以将字符串分隔为子字符串，以确定每个拆分的位置。[`split()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/String/split.md)

* **解题思路**：

![图](../../../public-repertory/img/other-algorithm-009-1.png)

将数字转为数组来判断，是比较简单的一种方法：

**首先**，我们将数字转成字符串，再转成数组。

**然后**，我们循环遍历这个数组。

**接着**，判断第 `i` 位和第 `length - (i + 1)` 位（例如 `1231`，第 `0` 位对应的是第 `length - 1` 位，第 `1` 位对应的是第 `length - 2` 位）。

**最后**，如果循环判断没问题，就返回 `true`；如果循环判断有问题，直接在循环中 `return false`。

### <a name="chapter-three-two" id="chapter-three-two">3.2 解法 - 数学算法</a>



* **解题代码**：

```js
var isPalindrome = function(x) {
  if(x < 0 || (x % 10 == 0 && x != 0)) {
    return false;
  }
  let revertedNumber = 0;
  while(x > revertedNumber) {
    revertedNumber = revertedNumber * 10 + x % 10;
    x = Math.floor(x / 10);
  }
  return x === revertedNumber || x === Math.floor(revertedNumber / 10);
};
```

* **执行测试**：

1. `x`：`12321`
2. `return`：

```js
true
```

* **LeetCode Submit**：

```js
✔ Accepted
  ✔ 11509/11509 cases passed (316 ms)
  ✔ Your runtime beats 97.12 % of javascript submissions
  ✔ Your memory usage beats 67.78 % of javascript submissions (45.5 MB)
```

* **知识点**：

1. `Math`：JS 中的内置对象，具有数学常数和函数的属性和方法。[`Math` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Math/README.md)

* **解题思路**：

![图](../../../public-repertory/img/other-algorithm-009-2.png)

**首先**，我们可以想象：当一个数的长度为偶数，那么它对折过来应该是相等的；当一个数的长度是奇数，那么它对折过来后，有一个的长度需要去掉一位数（除以 10 并取整），因为奇数长度的那个数，我们不需要判断它中间的数字。

> 我们定义传递过来的参数为：`x`，对折的数字为：`z`，而 `y` 为 `x` 目前的个位数。

**然后**，我们需要知道如何获取到一个数的个位数：`y = x % 10`，我们也需要知道如何将单个数字不断添加到一个数的末尾：`z = z * 10 + y`，例如：`z = 1 * 10 + 2 = 12`。

**接着**，我们只需要判断 `x` 是不是小于 `z` 了，毕竟当它小于的时候，说明数字已经对半或者过半了。

**最后**，我们判断一开始的两种情况，并返回 `true` 或者 `false` 即可。

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

