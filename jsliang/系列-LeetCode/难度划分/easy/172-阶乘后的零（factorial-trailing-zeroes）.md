172 - 阶乘后的零（factorial-trailing-zeroes）
===

> Create by **jsliang** on **2019-7-8 08:07:23**  
> Recently revised in **2019-7-8 09:14:41**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| [四 执行测试](#chapter-four) |
| [五 LeetCode Submit](#chapter-five) |
| [六 解题思路](#chapter-six) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：数学
* **题目地址**：https://leetcode-cn.com/problems/factorial-trailing-zeroes/
* **题目内容**：

```
给定一个整数 n，返回 n! 结果尾数中零的数量。

示例 1:
输入: 3
输出: 0
解释: 3! = 6, 尾数中没有零。

示例 2:
输入: 5
输出: 1
解释: 5! = 120, 尾数中有 1 个零.

说明: 你算法的时间复杂度应为 O(log n) 。
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var trailingZeroes = function(n) {
  let total = 0;
  while (n >= 5) {
    n = Math.floor(n / 5);
    total += n;
  }
  return total;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



1. `n`：`30`
2. `return`：`7`

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
√ Accepted
  √ 502/502 cases passed (80 ms)
  √ Your runtime beats 92.95 % of javascript submissions
  √ Your memory usage beats 68.18 % of javascript submissions (33.9 MB)
```

## <a name="chapter-six" id="chapter-six">六 解题思路</a>



**首先**，需要明确的是，这道题不能使用递归，因为超时了。

**然后**，这道题还需要考虑超限：

```js
var trailingZeroes = function(n) {
  let result = 1;
  while(n > 0) {
    result = result * n;
    n--;
  }
  result = result.toString().split('').reverse();
  for (let i = 0; i < result.length; i++) {
    if (result[i] !== '0') {
      return i;
    }
  }
  return 0;
};
```

在这份代码中，当你的数字为 30 的时候，你就超限了：

```js
× Wrong Answer
  × 21/502 cases passed (N/A)
  × testcase: '30'
  × answer: 0
  × expected_answer: 7
```

个人觉得这是正常思路，但是看到它这里显示 `21/502`，那么我就知道，它又想考我的智商了。

**智商税得交，谁让你数学没那么好呢！**

**接着**，咱访问下【评论】和【题解】，看看别人怎么破解，其中思路非常 nice 的是：

* https://leetcode-cn.com/problems/factorial-trailing-zeroes/solution/jie-cheng-hou-de-ling-die-dai-ji-di-gui-jie-fa-by-/

它的题解有两种：

> 题解 1 - 迭代

```js
var trailingZeroes = function(n) {
  let total = 0;
  while (n >= 5) {
    n = Math.floor(n / 5);
    total += n;
  }
  return total;
};
```

> 题解 2 - 递归

```js
var trailingZeroes = function(n) {
  const helper = (n, total) => {
    if (n < 5) {
      return total;
    }
    const count = Math.floor(n / 5);
    return helper(count, total + count);
  };
  return helper(n, 0);
};
```

那么，**jsliang** 看完题解，以自己意思表述一下：

**1**. 末尾有 0 是因为其中有 10 的因数，即 `2 * 5`、`1 * 10` 这种情况。

**2**. 找规律：当 `n` 为 5 时，有 1 个 0，当 `n` 为 10 时，有 2 个 0……但是，碰到某个特定的数时，会有意外，详情看表格：

| n | 个数 |
| --- | --- |
| 5 | 1 |
| 10 | 2 |
| 15 | 3 |
| 20 | 4 |
| 25 | 6 |
| 30 | 7 |
| 35 | 8 |
| 40 | 9 |
| 45 | 10 |
| 50 | 12 |

即当 `n` 为 25 倍数的时候，还需要将个数调整一次：

```js
var trailingZeroes = function(n) {
  let total = 0;
  while (n >= 5) {
    n = Math.floor(n / 5);
    total += n;
  }
  return total;
};
```

再结合题意，小伙伴们应该就比较清晰了。

**最后**，我们就得出了这道题的题解。

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

