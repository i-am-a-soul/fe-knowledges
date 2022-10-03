728 - 自除数（self-dividing-numbers）
===

> Create by **jsliang** on **2019-12-26 08:48:09**  
> Recently revised in **2019-12-26 09:04:16**

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
* **题目地址**：https://leetcode-cn.com/problems/self-dividing-numbers/
* **题目内容**：

```
自除数 是指可以被它包含的每一位数除尽的数。

例如，128 是一个自除数，
因为 128 % 1 == 0，128 % 2 == 0，128 % 8 == 0。

还有，自除数不允许包含 0 。

给定上边界和下边界数字，
输出一个列表，
列表的元素是边界（含边界）内所有的自除数。

示例 1：

输入： 
上边界left = 1, 
下边界right = 22
输出： [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 22]
注意：

每个输入参数的边界满足 1 <= left <= right <= 10000。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} left
 * @param {number} right
 * @return {number[]}
 */
var selfDividingNumbers = function(left, right) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 自除数
 * @param {number} left
 * @param {number} right
 * @return {number[]}
 */
const selfDividingNumbers = (left, right) => {
  const result = [];
  for (let item = left; item <= right; item++) {
    const temp = String(item);
    for (let j = 0; j < temp.length; j++) {
      if (temp % temp[j] !== 0) {
        break;
      }
      if (temp % temp[j] === 0 && j === temp.length - 1) {
        result.push(Number(temp));
      }
    }
  }
  return result;
};

console.log(selfDividingNumbers(1, 22));
```

`node index.js` 返回：

```js
[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 22 ]
```

## 四 LeetCode Submit



```js
Accepted
* 31/31 cases passed (72 ms)
* Your runtime beats 78.82 % of javascript submissions
* Your memory usage beats 57.63 % of javascript submissions (36.2 MB)
```

## 五 解题思路



数学题，要简单很简单，要难很难：

* **开始时间**：2019-12-26 08:48:12
* **结束时间**：2019-12-26 08:54:51

7 分钟搞定：

> 暴力破解

```js
/**
 * @name 自除数
 * @param {number} left
 * @param {number} right
 * @return {number[]}
 */
const selfDividingNumbers = (left, right) => {
  const result = [];
  for (let item = left; item <= right; item++) {
    const temp = String(item);
    for (let j = 0; j < temp.length; j++) {
      if (temp % temp[j] !== 0) {
        break;
      }
      if (temp % temp[j] === 0 && j === temp.length - 1) {
        result.push(Number(temp));
      }
    }
  }
  return result;
};
```

Submit 提交：

```js
Accepted
* 31/31 cases passed (72 ms)
* Your runtime beats 78.82 % of javascript submissions
* Your memory usage beats 57.63 % of javascript submissions (36.2 MB)
```

## 六 进一步思考



看到【题解区】有个 JavaScript 解法：

* https://leetcode-cn.com/problems/self-dividing-numbers/solution/mei-shi-yao-yao-zhuan-wan-liao-by-shetia/

做了下简化，如下所示：

> 【题解区】解法一

```js
const selfDividingNumbers = (left, right) => {
  const result = [];
  for (let item = left; item <= right; item++) {
    String(item).split('').every(t => item % t === 0) && result.push(item);
  }
  return result;
};
```

当然，这道题的简单难度无法想象，破解率 70%，所以小伙伴们随便折腾了。

如果小伙伴有更好的想法或者思路，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

