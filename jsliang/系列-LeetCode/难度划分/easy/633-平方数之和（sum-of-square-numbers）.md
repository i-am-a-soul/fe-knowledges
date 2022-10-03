633 - 平方数之和（sum-of-square-numbers）
===

> Create by **jsliang** on **2019-12-1 18:27:09**  
> Recently revised in **2019-12-1 19:38:20**

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
* **涉及知识**：数学
* **题目地址**：https://leetcode-cn.com/problems/sum-of-square-numbers/
* **题目内容**：

```
给定一个非负整数 c，
你要判断是否存在两个整数 a 和 b，
使得 a2 + b2 = c。

示例1:
输入: 5
输出: True
解释: 1 * 1 + 2 * 2 = 5

示例2:
输入: 3
输出: False
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} c
 * @return {boolean}
 */
var judgeSquareSum = function(c) {
  
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 平方数之和
 * @param {number} c
 * @return {boolean}
 */
const judgeSquareSum = (c) => {
  const sqrtNumber = Math.ceil(Math.sqrt(c));
  const map = new Map();
  for (let i = -sqrtNumber; i < sqrtNumber; i++) {
    const squareNumber = i * i;
    if (map.get(squareNumber) !== undefined) {
      return true;
    }
    map.set(c - squareNumber, i);
  }
  return c === 0 || false;
};

console.log(judgeSquareSum(5)); // true
console.log(judgeSquareSum(3)); // false
console.log(judgeSquareSum(2)); // true
console.log(judgeSquareSum(0)); // true
```

`node index.js` 返回：

```js
true
false
true
true
```

## 四 LeetCode Submit



```js
Accepted
* 124/124 cases passed (180 ms)
* Your runtime beats 8.46 % of javascript submissions
* Your memory usage beats 6.9 % of javascript submissions (61.6 MB)
```

## 五 解题思路



**首先**，拿到题目，不要慌乱，开始尝试：

```js
const judgeSquareSum = (c) => {
  const map = new Map();
  for (let i = 1; i < 5; i++) {
    if (
      map.get(i * i) !== undefined
      || i * i === c
    ) {
      return true;
    }
    if (i * i > c) {
      break;
    }
    map.set(c - i * i, i);
  }
  return false;
};
```

在这里，我们做的工作：

1. 设置 `Map` 记录哈希。
2. 遍历 `1` —— `c`。
3. 每个元素我们都设置它期待的值 `c - i * i` 为 `i`。例如 `c` 为 5 时，当遍历到 `1` 时，期待 `4`。
4. 判断当前的 `i * i` 是否出现了预期值，如果有，则返回 `true`。
5. 判断当前的 `i * i` 是否大于 `c`，如果是，说明循环不应持续下去了。

Submit 提交：

```
Wrong Answer
73/124 cases passed (N/A)

Testcase
2

Answer
false

Expected Answer
true
```

正常翻车，仔细看题：

```
给定一个非负整数 c ，你要判断是否存在两个整数 a 和 b，使得 a2 + b2 = c。
```

意思就是这两个整数 `a` 和 `b`，还可能是负整数和 0 咯，调整代码：

```js
const judgeSquareSum = (c) => {
  const sqrtNumber = Math.ceil(Math.sqrt(c));
  const map = new Map();
  for (let i = -sqrtNumber; i < sqrtNumber; i++) {
    const squareNumber = i * i;
    if (map.get(squareNumber) !== undefined) {
      return true;
    }
    map.set(c - squareNumber, i);
  }
  return c === 0 || false;
};
```

**然后**，Submit 提交：

```js
Accepted
* 124/124 cases passed (180 ms)
* Your runtime beats 8.46 % of javascript submissions
* Your memory usage beats 6.9 % of javascript submissions (61.6 MB)
```

**最后**，讲讲解题思路：

1. 众所周知如果不希望两个数的平方和大于某个数，那么它的范围应该是这个数开方后的数字。所以：`Math.ceil(Math.sqrt(c))`。
2. 使用 `map` 记录出现的数字期待的值。
3. 遍历 `[-sqrtNumber, -sqrtNumber]` 的范围，如果出现了哈希表匹对的数字，那么就是成功的。
4. `return` 的时候，还需要判断特殊条件 `0` 的情况。

## 六 进一步思考



得到上面 `8.46%` 和 `6.9%` 的答案，证明我这个哈希记录已经很失败了，思考下为什么：

1. 如果这个数特别大，例如 `10000`，那么我们查找的范围是 `[-100, 100]`，即 `200` 次。如果这个数再大点，那遍历的次数就多了。
2. 从小到大遍历，找的顺序是固定的，例如 10000，查找的是：`-100, -99, -98, ...0, 1, 2, ...98, 99, 100`。观察数字，你应当发现，我们做了很多无用功。

> 第一次优化

```js
const judgeSquareSum = (c) => {
  if (Number.isInteger(Math.sqrt(c))) {
    return true;
  }
  const sqrtNumber = Math.ceil(Math.sqrt(c));
  for (let i = 0; i < sqrtNumber; i++) {
    if (
      Number.isInteger(Math.sqrt(c - i * i))
      || i * i * 2 === c
    ) {
      return true;
    }
  }
  return false;
};
```

Submit 提交：

```js
Accepted
* 124/124 cases passed (72 ms)
* Your runtime beats 70.77 % of javascript submissions
* Your memory usage beats 20.69 % of javascript submissions (34.8 MB)
```

比起优化前的，稍微争气了一点点，继续尝试：

> 第二次优化

```js
const judgeSquareSum = (c) => {
  for (let i = 0; i * i <= c; i++) {
    if (Number.isInteger(Math.sqrt(c - i * i))) {
      return true;
    }
  }
  return false;
};
```

Submit 提交：

```js
Accepted
* 124/124 cases passed (60 ms)
* Your runtime beats 96.15 % of javascript submissions
* Your memory usage beats 20.69 % of javascript submissions (34.8 MB)
```

小脑袋瓜想不出更好的了，如果小伙伴有更好的思路或者想法，欢迎评论吐槽或者直接私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

