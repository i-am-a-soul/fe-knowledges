1237 - 找出给定方程的正整数解（find-positive-integer-solution-for-a-given-equation）
===

> Create by **jsliang** on **2020-02-01 11:18:10**  
> Recently revised in **2020-02-01 11:32:34**

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
* **涉及知识**：数学、二分查找
* **题目地址**：https://leetcode-cn.com/problems/find-positive-integer-solution-for-a-given-equation/
* **题目内容**：

```
给出一个函数  f(x, y) 和一个目标结果 z，
请你计算方程 f(x,y) == z 所有可能的正整数 数对 x 和 y。

给定函数是严格单调的，也就是说：

f(x, y) < f(x + 1, y)
f(x, y) < f(x, y + 1)

函数接口定义如下：

interface CustomFunction {
public:
  // Returns positive integer f(x, y) for any given positive integer x and y.
  int f(int x, int y);
};

如果你想自定义测试，
你可以输入整数 function_id 和一个目标结果 z 作为输入，
其中 function_id 表示一个隐藏函数列表中的一个函数编号，
题目只会告诉你列表中的 2 个函数。  

你可以将满足条件的 结果数对 按任意顺序返回。

示例 1：

输入：function_id = 1, z = 5
输出：[[1,4],[2,3],[3,2],[4,1]]
解释：function_id = 1 表示 f(x, y) = x + y

示例 2：

输入：function_id = 2, z = 5
输出：[[1,5],[5,1]]
解释：function_id = 2 表示 f(x, y) = x * y

提示：

1 <= function_id <= 9
1 <= z <= 100
题目保证 f(x, y) == z 的解处于 1 <= x, y <= 1000 的范围内。
在 1 <= x, y <= 1000 的前提下，
题目保证 f(x, y) 是一个 32 位有符号整数。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-positive-integer-solution-for-a-given-equation
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * // This is the CustomFunction's API interface.
 * // You should not implement it, or speculate about its implementation
 * function CustomFunction() {
 *
 *     @param {integer, integer} x, y
 *     @return {integer}
 *     this.f = function(x, y) {
 *         ...
 *     };
 *
 * };
 */
/**
 * @param {CustomFunction} customfunction
 * @param {integer} z
 * @return {integer[][]}
 */
var findSolution = function(customfunction, z) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * This is the CustomFunction's API interface.
 * You should not implement it, or speculate about its implementation
    function CustomFunction() {
      @param {integer, integer} x, y
      @return {integer}
      this.f = function(x, y) {
        ...
      };
    };
 */
/**
 * @name 找出给定方程的正整数解
 * @param {CustomFunction} customfunction
 * @param {integer} z
 * @return {integer[][]}
 */
const findSolution = (customfunction, z) => {
  const result = [];
  for (let i = 1; i <= z; i++) {
    for (let j = 1; j <= z; j++) {
      if (customfunction.f(i, j) === z) {
        result.push([i, j]);
      }
    }
  }
  return result;
};
```

## 四 LeetCode Submit



```js
Accepted
* 45/45 cases passed (64 ms)
* Your runtime beats 91.77 % of javascript submissions
* Your memory usage beats 60.15 % of javascript submissions (34.6 MB)
```

## 五 解题思路



由于题目包含了一个隐藏方法：`customfunction.f(x, y)`，所以如果测试那就需要提交测试了。

然后分析下题目：

1. 给定一个函数 `customfunction.f(x, y)`，给定一个期望值 `z` 为期望结果。
2. 计算符合 `[1, z]` 范围内，输出结果 `customfunction.f(x, y) === z` 的情况。

那么直接求解：

```js
const findSolution = (customfunction, z) => {
  const result = [];
  for (let i = 1; i <= z; i++) {
    for (let j = 1; j <= z; j++) {
      if (customfunction.f(i, j) === z) {
        result.push([i, j]);
      }
    }
  }
  return result;
};
```

简单来说，对这道题不太感冒，毕竟题目还是比较难以理解的（虽然答案很简单）。

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

