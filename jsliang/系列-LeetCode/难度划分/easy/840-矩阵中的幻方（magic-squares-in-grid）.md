840 - 矩阵中的幻方（magic-squares-in-grid）
===

> Create by **jsliang** on **2020-01-09 08:38:04**  
> Recently revised in **2020-01-09 09:28:45**

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
* **题目地址**：https://leetcode-cn.com/problems/magic-squares-in-grid/
* **题目内容**：

```
3 x 3 的幻方是一个填充有从 1 到 9 的不同数字的 3 x 3 矩阵，
其中每行，每列以及两条对角线上的各数之和都相等。

给定一个由整数组成的 grid，
其中有多少个 3 × 3 的 “幻方” 子矩阵？
（每个子矩阵都是连续的）。

示例：

输入: [[4,3,8,4],
      [9,5,1,9],
      [2,7,6,2]]
输出: 1
解释: 
下面的子矩阵是一个 3 x 3 的幻方：
438
951
276

而这一个不是：
384
519
762

总的来说，
在本示例所给定的矩阵中只有一个 3 x 3 的幻方子矩阵。

提示:
1 <= grid.length <= 10
1 <= grid[0].length <= 10
0 <= grid[i][j] <= 15
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var numMagicSquaresInside = function(grid) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 判断是否为幻方
 * @param {number[][]} grid 模仿
 * @param {number} i 横坐标
 * @param {number} j 纵坐标
 */
const judgeMagicSquars = (grid, i, j) => {
  const nowMagicSquars = [
    grid[i][j], grid[i + 1][j], grid[i + 2][j], // 第一排
    grid[i][j + 1], grid[i + 1][j + 1], grid[i + 2][j + 1], // 第二排
    grid[i][j + 2], grid[i + 1][j + 2], grid[i + 2][j + 2], // 第三排
  ];
  // 判断是否重叠数字，例如 [[5, 5, 5], [5, 5, 5], [5, 5, 5]]
  if ([...new Set(nowMagicSquars)].length !== 9) {
    return false;
  }
  // 判断是否超过限制，例如 0 或者大于 9 的数字
  if (nowMagicSquars.filter(i => i > 9 || i === 0).length) {
    return false;
  }
  const row1 = grid[i][j] + grid[i + 1][j] + grid[i + 2][j]; // 第一横排
  return (
    row1 === grid[i][j + 1] + grid[i + 1][j + 1] + grid[i + 2][j + 1] // 第二横排
    && row1 === grid[i][j + 2] + grid [i + 1][j + 2] + grid[i + 2][j + 2] // 第三横排
    && row1 === grid[i][j] + grid[i][j + 1] + grid[i][j + 2] // 第一竖排
    && row1 === grid[i + 1][j] + grid[i + 1][j + 1] + grid[i + 1][j + 2] // 第二竖排
    && row1 === grid[i + 2][j] + grid[i + 2][j + 1] + grid[i + 2][j + 2] // 第三竖排
    && row1 === grid[i][j] + grid[i + 1][j + 1] + grid[i + 2][j + 2] // 顺对角线
    && row1 === grid[i + 2][j] + grid[i + 1][j + 1] + grid[i][j + 2] // 逆对角线
  );
};

/**
 * @name 矩阵中的幻方
 * @param {number[][]} grid
 * @return {number}
 */
const numMagicSquaresInside = (grid) => {
  let count = 0;
  for (let i = 0; i < grid.length - 2; i++) {
    for (let j = 0; j < grid[i].length - 2; j++) {
      if (judgeMagicSquars(grid, i, j)) {
        count ++;
      }
    }
  }
  return count;
};

console.log(numMagicSquaresInside(
  [
    [4, 3, 8, 4],
    [9, 5, 1, 9],
    [2, 7, 6, 2],
    [1, 4, 8, 9]
  ]
));
```

`node index.js` 返回：

```js
1
```

## 四 LeetCode Submit



```js
Accepted
* 91/91 cases passed (84 ms)
* Your runtime beats 27.91 % of javascript submissions
* Your memory usage beats 10 % of javascript submissions (37.5 MB)
```

## 五 解题思路



陷阱：

```
3 x 3 的幻方是一个填充有从 1 到 9 的不同数字的 3 x 3 矩阵


0 <= grid[i][j] <= 15
```

它说矩阵是 [1, 9]，后面给出的感觉像是 [0, 15]，所以需要关注下。

> 暴力破解

```js
const judgeMagicSquars = (grid, i, j) => {
  const nowMagicSquars = [
    grid[i][j], grid[i + 1][j], grid[i + 2][j], // 第一排
    grid[i][j + 1], grid[i + 1][j + 1], grid[i + 2][j + 1], // 第二排
    grid[i][j + 2], grid[i + 1][j + 2], grid[i + 2][j + 2], // 第三排
  ];
  // 判断是否重叠数字，例如 [[5, 5, 5], [5, 5, 5], [5, 5, 5]]
  if ([...new Set(nowMagicSquars)].length !== 9) {
    return false;
  }
  // 判断是否超过限制，例如 0 或者大于 9 的数字
  if (nowMagicSquars.filter(i => i > 9 || i === 0).length) {
    return false;
  }
  const row1 = grid[i][j] + grid[i + 1][j] + grid[i + 2][j]; // 第一横排
  return (
    row1 === grid[i][j + 1] + grid[i + 1][j + 1] + grid[i + 2][j + 1] // 第二横排
    && row1 === grid[i][j + 2] + grid [i + 1][j + 2] + grid[i + 2][j + 2] // 第三横排
    && row1 === grid[i][j] + grid[i][j + 1] + grid[i][j + 2] // 第一竖排
    && row1 === grid[i + 1][j] + grid[i + 1][j + 1] + grid[i + 1][j + 2] // 第二竖排
    && row1 === grid[i + 2][j] + grid[i + 2][j + 1] + grid[i + 2][j + 2] // 第三竖排
    && row1 === grid[i][j] + grid[i + 1][j + 1] + grid[i + 2][j + 2] // 顺对角线
    && row1 === grid[i + 2][j] + grid[i + 1][j + 1] + grid[i][j + 2] // 逆对角线
  );
};

const numMagicSquaresInside = (grid) => {
  let count = 0;
  for (let i = 0; i < grid.length - 2; i++) {
    for (let j = 0; j < grid[i].length - 2; j++) {
      if (judgeMagicSquars(grid, i, j)) {
        count ++;
      }
    }
  }
  return count;
};
```

思路如下：

1. 判断坐标，我们只需要或者 9 宫格的起始位置就行了，所以必定小于横纵坐标 - 2 的坐标。
2. 在 `judgeMagicSquars` 方法体中：
3. 通过 `nowMagicSquars` 获取当前九宫格的 9 个数字，判断它是否重复或者它超过了幻方的规矩（num === 0 || num > 9），如果是，则判断这不是一个合格的幻方。
4. 最后判断横排、纵排、对角线的和是否和第一横排的值相等。

这样，就完成了这道题的暴力破解：

```js
Accepted
* 91/91 cases passed (84 ms)
* Your runtime beats 27.91 % of javascript submissions
* Your memory usage beats 10 % of javascript submissions (37.5 MB)
```

效率极其低下！

## 六 进一步思考



解题辈有大佬出，看到大佬题解：

> 超暴力破解

```js
const numMagicSquaresInside = (grid) => {
  // 暴力将所有幻方情况列举出来
  const magicSquareList = [
    '[8,1,6,3,5,7,4,9,2]',
    '[6,1,8,7,5,3,2,9,4]',
    '[4,9,2,3,5,7,8,1,6]',
    '[2,9,4,7,5,3,6,1,8]',
    '[6,7,2,1,5,9,8,3,4]',
    '[8,3,4,1,5,9,6,7,2]',
    '[2,7,6,9,5,1,4,3,8]',
    '[4,3,8,9,5,1,2,7,6]'
  ]
  let count = 0;
  for (let i = 0; i < grid.length - 2; i++) {
    for (let j = 0; j < grid[0].length - 2; j++) {
      const temp = '[' +
        grid[i][j] + ',' + grid[i][j+1] + ',' + grid[i][j+2] + ',' +
        grid[i+1][j] + ',' + grid[i+1][j+1] + ',' + grid[i+1][j+2] + ',' +
        grid[i+2][j] + ',' + grid[i+2][j+1] + ',' + grid[i+2][j+2]
      + ']';
      if (magicSquareList.includes(temp)) {
        count++
      }
    }
  }
  return count;
};
```

我也不管你怎么搞，反正我知道幻方排列组合共有 8 种，我都列举出来。

然后判断当前点所在的 9 宫格是不是属于这 8 种情况之一就行！

Submit 提交：

```js
Accepted
* 91/91 cases passed (76 ms)
* Your runtime beats 46.51 % of javascript submissions
* Your memory usage beats 10 % of javascript submissions (36.7 MB)
```

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

