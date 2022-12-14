509 - 斐波那契数列（fibonacci-number）
===

> Create by **jsliang** on **2019-11-04 09:12:19**  
> Recently revised in **2019-11-04 09:36:09**

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题及测试](#chapter-three) |
| [四 LeetCode Submit](#chapter-four) |
| [五 解题思路](#chapter-five) |
| [六 进一步思考](#chapter-six) |

## 二 前言



* **难度**：简单
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/fibonacci-number/
* **题目内容**：

```
斐波那契数，通常用 F(n) 表示，形成的序列称为斐波那契数列。该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。也就是：

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
给定 N，计算 F(N)。

示例 1：
输入：2
输出：1
解释：F(2) = F(1) + F(0) = 1 + 0 = 1.

示例 2：
输入：3
输出：2
解释：F(3) = F(2) + F(1) = 1 + 1 = 2.

示例 3：
输入：4
输出：3
解释：F(4) = F(3) + F(2) = 2 + 1 = 3.
 

提示：
0 ≤ N ≤ 30
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} N
 * @return {number}
 */
var fib = function(N) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 斐波那契数列
 * @param {number} N
 * @return {number}
 */
const fib = (N) => {
  const list = [0, 1];
  for (let i = 2; i <= N; i++) {
    list[i] = list[i - 1] + list[i - 2];
  }
  return list[N];
};
```

`node index.js` 返回：

```js
5
```

## 四 LeetCode Submit



```js
Accepted
* 31/31 cases passed (64 ms)
* Your runtime beats 88.55 % of javascript submissions
* Your memory usage beats 74.63 % of javascript submissions (33.6 MB)
```

## 五 解题思路



拿到题目，思考思路：

1. 暴力破解。从第二项开始算到第 N 项即可。
2. 超暴力输出。直接算出 0-N 的斐波那契数列，然后返回 `result[N]` 即可。
3. 递归。通过递归的方式，给出结果。

那么，开始试验：

> 暴力破解

```js
const fib = (N) => {
  const list = [0, 1];
  for (let i = 2; i <= N; i++) {
    list[i] = list[i - 1] + list[i - 2];
  }
  return list[N];
};

const N = 5;
console.log(fib(N));
```

Submit 提交结果：

```js
Accepted
* 31/31 cases passed (64 ms)
* Your runtime beats 88.55 % of javascript submissions
* Your memory usage beats 74.63 % of javascript submissions (33.6 MB)
```

> 超暴力输出

```js
const fib = (N) => {
  const list = [ 0,
    1,
    1,
    2,
    3,
    5,
    8,
    13,
    21,
    34,
    55,
    89,
    144,
    233,
    377,
    610,
    987,
    1597,
    2584,
    4181,
    6765,
    10946,
    17711,
    28657,
    46368,
    75025,
    121393,
    196418,
    317811,
    514229,
    832040 ];
  return list[N];
};
```

Submit 提交结果：

```js
Accepted
* 31/31 cases passed (60 ms)
* Your runtime beats 94.52 % of javascript submissions
* Your memory usage beats 55.12 % of javascript submissions (33.7 MB)
```

> 递归

```js
const fib = (N) => {
  if (N === 0) {
    return 0;
  }
  if (N === 1) {
    return 1;
  }
  return fib(N - 1) + fib(N - 2);
};
```

Submit 提交结果：

```js
Accepted
* 31/31 cases passed (92 ms)
* Your runtime beats 32.03 % of javascript submissions
* Your memory usage beats 9.27 % of javascript submissions (34.1 MB)
```

超嗨皮的早上醒来直接三种方式解题，感觉非常熟练啊~

## 六 进一步思考



那么，除了这三种方法，还有没有其他方法呢？

期待小伙伴们的评论吐槽或者微信私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

