746 - 使用最小花费爬楼梯（min-cost-climbing-stairs）
===

> Create by **jsliang** on **2019-12-30 08:37:35**  
> Recently revised in **2019-12-30 09:50:28**

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
* **涉及知识**：数组、动态规划
* **题目地址**：https://leetcode-cn.com/problems/min-cost-climbing-stairs/
* **题目内容**：

```
数组的每个索引做为一个阶梯，
第 i 个阶梯对应着一个非负数的体力花费值 cost[i](索引从 0 开始)。

每当你爬上一个阶梯你都要花费对应的体力花费值，
然后你可以选择继续爬一个阶梯或者爬两个阶梯。

您需要找到达到楼层顶部的最低花费。

在开始时，
你可以选择从索引为 0 或 1 的元素作为初始阶梯。

示例 1:

输入: cost = [10, 15, 20]
输出: 15
解释: 最低花费是从 cost[1] 开始，
然后走两步即可到阶梯顶，一共花费 15。

示例 2:

输入: cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
输出: 6
解释: 最低花费方式是从 cost[0] 开始，
逐个经过那些 1，跳过 cost[3]，一共花费 6。

注意：

cost 的长度将会在 [2, 1000]。
每一个 cost[i] 将会是一个 Integer 类型，范围为 [0, 999]。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var islandPerimeter = function(grid) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 使用最小花费爬楼梯
 * @param {number[]} cost
 * @return {number}
 */
const minCostClimbingStairs = (cost) => {
  let result1 = 0,
      result2 = 0;
  for (let i = cost.length - 1; i >= 0; i--) {
    const temp = cost[i] + Math.min(result1, result2);
    result2 = result1;
    result1 = temp;
  }
  return Math.min(result1, result2);
};

console.log(minCostClimbingStairs([10, 15, 20])); // 15
console.log(minCostClimbingStairs([1, 100, 1, 1, 1, 100, 1, 1, 100, 1])); // 6
```

`node index.js` 返回：

```js
15
6
```

## 四 LeetCode Submit



```js
Accepted
* 276/276 cases passed (72 ms)
* Your runtime beats 66.09 % of javascript submissions
* Your memory usage beats 47.83 % of javascript submissions (35.4 MB)
```

## 五 解题思路



因为这道题标明是动态规划，又因为我这方面知识欠缺，所以就去搜索了下动态规划的玩法。

然后呢，值得注意的是，如果你网上翻到的文章，只讲下面这几块内容，就不用往下翻了，浪费时间：

1. 斐波那契数列
2. 最长公共子序列

在这里推荐几篇文章：

1. [动态规划难？读完这篇还不理解那就不要请我吃鸡了 -  zy445566](https://cnodejs.org/topic/5c1b091176c4964062a1ba44)
2. [JavaScript 版动态规划算法题：打家劫舍 - 刘一奇](https://www.liuyiqi.cn/2017/03/10/house-robber/)

当然，看完我还是不懂我这道题怎么解，先暴力试试：

> 暴力破解

```js
// 愣是没想出来
```

一想到还有动态规划这么巧妙的方法，就忍不住去想怎么解。

一开始的思路是顺序遍历，取前三者中最小一个 `i + 1` 或者最小两个 `i + (i + 2)`，但是想想我还要定位每次加到哪了，就嫌麻烦。

看了下官方题解，豁然开朗：

```js
const minCostClimbingStairs = (cost) => {
  let result1 = 0,
      result2 = 0;
  for (let i = cost.length - 1; i >= 0; i--) {
    const temp = cost[i] + Math.min(result1, result2);
    result2 = result1;
    result1 = temp;
  }
  return Math.min(result1, result2);
};
```

看代码，其实想法很简单，就是想不出来：

1. 最少的应该是 `cost[i] + min(f[f + 1], f[f + 2])`。即当前项和前两项中最小的相加。
2. 因为顺序遍历来说不方便，所以需要倒序遍历。
3. 通过 `result1 = f[f + 1]`，`result2 = f[f + 2]`，我们倒序相加。

最终输出结果：

```js
Accepted
* 276/276 cases passed (72 ms)
* Your runtime beats 66.09 % of javascript submissions
* Your memory usage beats 47.83 % of javascript submissions (35.4 MB)
```

真真想不到系列，看来【动态规划】还需要多练习一下，了解了解玄学~

如果小伙伴有更好的想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

