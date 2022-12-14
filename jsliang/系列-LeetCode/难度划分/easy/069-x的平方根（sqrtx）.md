069 - x 的平方根（sqrtx）
===

> Create by **jsliang** on **2019-06-11 15:17:21**  
> Recently revised in **2019-09-18 10:20:48**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| &emsp;[3.1 解题 - JS API](#chapter-three-one) |
| &emsp;[3.2 解法 - 暴力破解](#chapter-three-two) |
| &emsp;[3.3 解法 - 二分查找](#chapter-three-three) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：数学、二分查找
* **题目地址**：https://leetcode-cn.com/problems/sqrtx/
* **题目内容**：

```
实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

示例 1:
输入: 4
输出: 2

示例 2:
输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 讲解下使用 JavaScript 的解题思路。

### <a name="chapter-three-one" id="chapter-three-one">3.1 解法 - JS API</a>



* **解题代码**：

```js
var mySqrt = function(x) {
  return Math.floor(Math.sqrt(x));
};
```

* **执行测试**：

1. `x`：`8`
2. `return`：

```js
2
```

* **LeetCode Submit**：

```js
✔ Accepted
  ✔ 1017/1017 cases passed (92 ms)
  ✔ Your runtime beats 98.33 % of javascript submissions
  ✔ Your memory usage beats 77.02 % of javascript submissions (35.3 MB)
```

* **知识点**：

1. `Math`：JS 中的内置对象，具有数学常数和函数的属性和方法。[`Math` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Math/README.md)

* **解题思路**：

直接使用 JS 原生 API 刷题，帅的嘛就不谈了，一分钟看题，两分钟解题，一分钟测试，搞定！

### <a name="chapter-three-two" id="chapter-three-two">3.2 解法 - 暴力破解</a>



* **解题代码**：

```js
var mySqrt = function(x) {
  if (x === 0 || x === 1) {
    return x;
  }
  for (let i = 0; i < x; i++) {
    if (i * i <= x && (i + 1) * (i + 1) > x) {
      return i;
    }
  }
};
```

* **执行测试**：

1. `x`：`8`
2. `return`：

```js
2
```

* **LeetCode Submit**：

```js
✔ Accepted
  ✔ 1017/1017 cases passed (200 ms)
  ✔ Your runtime beats 14.4 % of javascript submissions
  ✔ Your memory usage beats 39.85 % of javascript submissions (35.7 MB)
```

* **解题思路**：

**暴力破解一时爽，一直暴力一直爽**！

思路非常简单，由于忽略了负数情况，所以直接：`i² <= x <= (i+1)²` 即可。

不过暴力破解忽略了时间和空间，所以效率是相当低下。

* **进一步思考**：

### <a name="chapter-three-three" id="chapter-three-three">3.3 解法 - 二分查找</a>



* **解题代码**：

```js
var mySqrt = function(x) {
  if (x === 0 || x === 1) {
    return x;
  }
  let left = 1;
  let right = x;
  while (left <= right) {
    let middle = Math.floor((left + right) / 2);
    if (middle * middle > x) {
      right = middle;
    }
    if (middle * middle < x) {
      left = middle;
    }
    if (middle * middle === x) {
      return middle;
    }
    if (left === right - 1 && left * left <= x && right * right >= x) {
      return left;
    }
  }
};
```

* **执行测试**：

1. `x`：`8`
2. `return`：

```js
2
```

* **LeetCode Submit**：

```js
✔ Accepted
  ✔ 1017/1017 cases passed (92 ms)
  ✔ Your runtime beats 98.33 % of javascript submissions
  ✔ Your memory usage beats 19.07 % of javascript submissions (35.9 MB)
```

* **知识点**：

1. `Math`：JS 中的内置对象，具有数学常数和函数的属性和方法。[`Math` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Math/README.md)

* **解题思路**：

**首先**，判断是不是 `0` 或者 `1` 这两种特殊情况，如果是，则返回这两个数字。

**然后**，开始二分，设置左侧为 `1`，右侧范围为 `x`，形成闭区间 `[1, x]`（数学表示，而不是数组）。

1. 输入 `8`，形成闭区间 `[1, 8]`。
2. 第一次遍历，`Math.floor((1 + 8) / 2)` 的值为 `4`，因为 `4 * 4 = 16`，该值大于 `8`，所以这时候闭区间变成：`[1, 4]`。
3. 第二次遍历，`Math.floor((1 + 4) / 2)` 的值为 `2`，因为 `2 * 2 = 4`，该值小于 `8`，所以这时候闭区间变成：`[2, 4]`。
4. 第三次遍历，`Math.floor((1 + 4) / 2)` 的值为 `3`，因为 `3 * 3 = 9`，该值大于 `8`，所以这时候闭区间变成：`[2, 3]`。
5. 此时，因为 `2 === 3 - 1 && 2² <= 8 && 3² > 8`，所以我们找到了最终值，即 `2`。

**最后**，我们便通过三种方法：JS 原生 API、暴力破解、二分法，完成了本次解题。

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

