1252 - 奇数值单元格的数目（cells-with-odd-values-in-a-matrix）
===

> Create by **jsliang** on **2020-02-01 11:34:49**  
> Recently revised in **2020-02-01 13:17:38**

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
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/cells-with-odd-values-in-a-matrix/
* **题目内容**：

给你一个 n 行 m 列的矩阵，最开始的时候，每个单元格中的值都是 0。

另有一个索引数组 indices，indices[i] = [ri, ci] 中的 ri 和 ci 分别表示指定的行和列（从 0 开始编号）。

你需要将每对 [ri, ci] 指定的行和列上的所有单元格的值加 1。

请你在执行完所有 indices 指定的增量操作后，返回矩阵中 「奇数值单元格」 的数目。

示例 1：

![图](../../../public-repertory/img/other-algorithm-1252-1.png)

* 输入：n = 2, m = 3, indices = [[0,1],[1,1]]
* 输出：6
* 解释：

```
最开始的矩阵是 [[0,0,0],[0,0,0]]。
第一次增量操作后得到 [[1,2,1],[0,1,0]]。
最后的矩阵是 [[1,3,1],[1,3,1]]，里面有 6 个奇数。
```

示例 2：

![图](../../../public-repertory/img/other-algorithm-1252-2.png)

* 输入：n = 2, m = 2, indices = [[1,1],[0,0]]
* 输出：0
* 解释：最后的矩阵是 [[2,2],[2,2]]，里面没有奇数。
 
提示：

1. 1 <= n <= 50
2. 1 <= m <= 50
3. 1 <= indices.length <= 100
4. 0 <= indices[i][0] < n
5. 0 <= indices[i][1] < m

* 来源：力扣（LeetCode）
* 链接：https://leetcode-cn.com/problems/cells-with-odd-values-in-a-matrix
* 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} n
 * @param {number} m
 * @param {number[][]} indices
 * @return {number}
 */
var oddCells = function(n, m, indices) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 奇数值单元格的数目
 * @param {number} n
 * @param {number} m
 * @param {number[][]} indices
 * @return {number}
 */
const oddCells = (n, m, indices) => {
  // 1. 初始化矩阵
  const matrix = Array.from(Array(n), () => Array.from(Array(m), () => 0));
  // 2. 渲染矩阵
  for (let i = 0; i < indices.length; i++) {
    const pointX = indices[i][0];
    const pointY = indices[i][1];
    for (let j = 0; j < m; j++) {
      matrix[pointX][j] += 1;
    }
    for (let k = 0; k < n; k++) {
      matrix[k][pointY] += 1;
    }
  }
  // 3. 统计奇数
  let result = 0;
  for (let i = 0; i < matrix.length; i++) {
    for (let j = 0; j < matrix[i].length; j++) {
      if (matrix[i][j] % 2 === 1) {
        result++;
      }
    }
  }
  return result;
};

console.log(oddCells(2, 3, [[0, 1], [1, 1]]));
```

`node index.js` 返回：

```js
6
```

## 四 LeetCode Submit



```js
Accepted
* 44/44 cases passed (72 ms)
* Your runtime beats 64.18 % of javascript submissions
* Your memory usage beats 26.19 % of javascript submissions (36.3 MB)
```

## 五 解题思路



拿到题目，分析题意：

1. 有个 `n * m` 的矩阵，里面的数一开始都是 0。
2. 有个数组 `indices`，其中对于每项 `i` 来说，`x = indices[i][0]` 代表我们要将第 `x` 行的数字都 + 1；`y = indices[i][1]` 代表我们要将第 `y` 列的数字都 + 1。
3. 统计 `n * m` 的矩阵中，渲染的数字为奇数的个数。

> 暴力破解

```js
const oddCells = (n, m, indices) => {
  // 1. 初始化矩阵
  const matrix = Array.from(Array(n), () => Array.from(Array(m), () => 0));
  // 2. 渲染矩阵
  for (let i = 0; i < indices.length; i++) {
    const pointX = indices[i][0];
    const pointY = indices[i][1];
    for (let j = 0; j < m; j++) {
      matrix[pointX][j] += 1;
    }
    for (let k = 0; k < n; k++) {
      matrix[k][pointY] += 1;
    }
  }
  // 3. 统计奇数
  let result = 0;
  for (let i = 0; i < matrix.length; i++) {
    for (let j = 0; j < matrix[i].length; j++) {
      if (matrix[i][j] % 2 === 1) {
        result++;
      }
    }
  }
  return result;
};
```

Submit 提交：

```js
Accepted
* 44/44 cases passed (72 ms)
* Your runtime beats 64.18 % of javascript submissions
* Your memory usage beats 26.19 % of javascript submissions (36.3 MB)
```

当然，肯定还有啥奇技淫巧，这里小伙伴们有兴趣的可以探索尝试下。

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

