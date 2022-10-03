073 - 矩阵置零（set-matrix-zeroes）
===

> Create by **jsliang** on **2019-08-09 10:43:32**  
> Recently revised in **2019-09-18 14:18:51**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| [四 执行测试](#chapter-four) |
| [五 LeetCode Submit](#chapter-five) |
| [六 知识点](#chapter-six) |
| [七 解题思路](#chapter-seven) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：中等
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/set-matrix-zeroes/
* **题目内容**：

```
给定一个 m x n 的矩阵，如果一个元素为 0，则将其所在行和列的所有元素都设为 0。请使用原地算法。

示例 1:

输入: 
[
  [1,1,1],
  [1,0,1],
  [1,1,1]
]
输出: 
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]

示例 2:

输入: 
[
  [0,1,2,0],
  [3,4,5,2],
  [1,3,1,5]
]
输出: 
[
  [0,0,0,0],
  [0,4,5,0],
  [0,3,1,0]
]

进阶:

一个直接的解决方案是使用  O(mn) 的额外空间，但这并不是一个好的解决方案。
一个简单的改进方案是使用 O(m + n) 的额外空间，但这仍然不是最好的解决方案。

你能想出一个常数空间的解决方案吗？
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
const setZeroes = (matrix) => {
  // 每排的长度
  const rowLength = matrix[0].length;
  // 总共有几排
  const verticalLength = matrix.length;
  // 标记 0 的数组
  let mark = [];
  // 遍历矩阵，将 0 都找出来。
  for (let i = 0; i < verticalLength; i++) {
    let zeroIndexList = [];
    for (let j = 0; j < rowLength; j++) {
      if (matrix[i][j] === 0) {
        zeroIndexList.push(j);
      }
    }
    mark.push(zeroIndexList);
  }
  // 遍历标记数组，修改对应的矩阵
  for (let i = 0; i < verticalLength; i++) {
    if (mark[i].length) {
      // 计算横排
      matrix[i] = new Array(rowLength).fill(0);
      // 计算竖排
      mark[i].forEach((item) => {
        for (let i = 0; i < verticalLength; i++) {
          matrix[i][item] = 0;
        }
      })
    }
  }
  return matrix;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



* `matrix`：

```js
let matrix = [
  [1,1,1],
  [1,0,1],
  [1,1,1]
];
```

* `return`：

```js
[
  [ 1, 0, 1 ],
  [ 0, 0, 0 ],
  [ 1, 0, 1 ]
]
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
✔ Accepted
  ✔ 159/159 cases passed (128 ms)
  ✔ Your runtime beats 74.67 % of javascript submissions
  ✔ Your memory usage beats 8.33 % of javascript submissions (37.9 MB)
```

## <a name="chapter-six" id="chapter-six">六 知识点</a>



1. `push()`：`push()` 方法将一个或多个元素添加到数组的末尾，并返回该数组的新长度。[`push()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Array/push.md)
2. `fill()`：`fill()` 方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。[`fill()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Array/fill.md)
3. `forEach()`：`forEach()` 方法对数组的每个元素执行一次提供的函数。[`forEach()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Array/forEach.md)

## <a name="chapter-seven" id="chapter-seven">七 解题思路</a>



**首先**，就我这榆木脑袋，肯定不撞南墙不回头，先暴力试试：

```js
const setZeroes = (matrix) => {
  const rowLength = matrix[0].length;
  const verticalLength = matrix.length;
  let temp = [];
  for (let i = 0; i < verticalLength; i++) {
    let zeroIndexList = [];
    for (let j = 0; j < rowLength; j++) {
      if (matrix[i][j] === 0) {
        zeroIndexList.push(j);
      }
    }
    temp.push(zeroIndexList);
  }
  for (let i = 0; i < verticalLength; i++) {
    if (temp[i].length) {
      // 计算横排
      matrix[i] = new Array(rowLength).fill(0);
      // 计算竖排
      temp[i].forEach((item) => {
        for (let i = 0; i < verticalLength; i++) {
          matrix[i][item] = 0;
        }
      })
    }
  }
  return matrix;
};
```

思路比较复杂点：

1. 用 `rowLength` 记录横排长度，用 `verticalLength` 记录纵排长度。
2. 用 `temp` 记录 0 出现的情况。
3. 遍历 `temp`，当某行出现 0 的时候，我们就依题意进行 0 设置。

提交看看：

```js
✔ Accepted
  ✔ 159/159 cases passed (120 ms)
  ✔ Your runtime beats 89.33 % of javascript submissions
  ✔ Your memory usage beats 6.66 % of javascript submissions (37.9 MB)
```

立即成功~

> 当然，中间尝试了几遍，就不说出来了。

**然后**，咱们想想优化方案：

```js
const setZeroes = (matrix) => {
  // 每排的长度
  const rowLength = matrix[0].length;
  // 总共有几排
  const verticalLength = matrix.length;
  // 标记 0 的数组
  let mark = [];
  // 遍历矩阵，将 0 都找出来。
  for (let i = 0; i < verticalLength; i++) {
    let zeroIndexList = [];
    for (let j = 0; j < rowLength; j++) {
      if (matrix[i][j] === 0) {
        zeroIndexList.push(j);
      }
    }
    mark.push(zeroIndexList);
  }
  // 遍历标记数组，修改对应的矩阵
  for (let i = 0; i < verticalLength; i++) {
    if (mark[i].length) {
      // 计算横排
      matrix[i] = new Array(rowLength).fill(0);
      // 计算竖排
      mark[i].forEach((item) => {
        for (let i = 0; i < verticalLength; i++) {
          matrix[i][item] = 0;
        }
      })
    }
  }
  return matrix;
};
```

写死了~只要写写注释了。

**最后**，翻了下【评论】和【题解】，我 JS 大佬呢，怎么没看到非常优秀的题解？伤心~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

