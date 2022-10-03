342 - 4的幂（power-of-four）
===

> Create by **jsliang** on **2019-07-22 18:43:57**  
> Recently revised in **2019-07-22 18:55:02**

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
* **涉及知识**：位运算
* **题目地址**：https://leetcode.com/problems/power-of-four/
* **题目内容**：

```
Given an integer (signed 32 bits), write a function to check whether it is a power of 4.

Example 1:
Input: 16
Output: true

Example 2:
Input: 5
Output: false

Follow up: Could you solve it without loops/recursion?
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var isPowerOfFour = function(num) {
  while (num > 4) {
    num = num / 4;
  }
  if (num === 4 || num === 1) {
    return true;
  } else {
    return false;
  }
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



1. `num`：`64`
2. `return`：

```js
true
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
Success
Runtime: 72 ms, faster than 68.45% of JavaScript online submissions for Power of Four.
Memory Usage: 35.5 MB, less than 98.97% of JavaScript online submissions for Power of Four.
```

## <a name="chapter-six" id="chapter-six">六 解题思路</a>



**首先**，刚好看到 LeetCode 崩溃的一幕，所以去英文官网找题做了。

**然后**，这道题的题解跟 231-2的幂 以及 326-3的幂 重复了，感觉 LeetCode 是不是有点黔驴技穷。

**最后**，这道题的题解即是通过循环得到最终数，判断是否为 4 或者 1 即可。

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

