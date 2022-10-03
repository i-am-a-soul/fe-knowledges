661 - 图片平滑器（image-smoother）
===

> Create by **jsliang** on **2019-12-07 08:47:40**  
> Recently revised in **2019-12-07 09:42:53**

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
* **题目地址**：https://leetcode-cn.com/problems/image-smoother/
* **题目内容**：

```
包含整数的二维矩阵 M 表示一个图片的灰度。

你需要设计一个平滑器来让每一个单元的灰度成为平均灰度 (向下舍入) ，

平均灰度的计算是周围的8个单元和它本身的值求平均，

如果周围的单元格不足八个，则尽可能多的利用它们。

示例 1:

输入:
[[1,1,1],
 [1,0,1],
 [1,1,1]]

输出:
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]

解释:
对于点 (0,0), (0,2), (2,0), (2,2): 
  平均(3/4) = 平均(0.75) = 0
对于点 (0,1), (1,0), (1,2), (2,1):
   平均(5/6) = 平均(0.83333333) = 0
对于点 (1,1): 
  平均(8/9) = 平均(0.88888889) = 0

注意:
给定矩阵中的整数范围为 [0, 255]。
矩阵的长和宽的范围均为 [1, 150]。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[][]} M
 * @return {number[][]}
 */
var imageSmoother = function(M) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 图片平滑器
 * @param {number[][]} M
 * @return {number[][]}
 */
const imageSmoother = (M) => {
  const newM = [];
  for(let i = 0; i < M.length; i++) {
    console.log(`---${M[i]}---`);
    newM[i] = [];
    for (let j = 0; j < M[i].length; j++) {
      let result = 0;
      let count = 0;
      // 左上角
      if (M[i - 1] && M[i - 1][j + 1] !== undefined) {
        result += M[i - 1][j + 1];
        count += 1;
      }
      // 上方
      if (M[i] && M[i][j + 1] !== undefined) {
        result += M[i][j + 1];
        count += 1;
      }
      // 右上角
      if (M[i + 1] && M[i + 1][j + 1] !== undefined) {
        result += M[i + 1][j + 1];
        count += 1;
      }
      // 左边
      if (M[i - 1] && M[i - 1][j] !== undefined) {
        result += M[i - 1][j];
        count += 1;
      }
      // 正中间
      if (M[i] && M[i][j] !== undefined) {
        result += M[i][j];
        count += 1;
      }
      // 右边
      if (M[i + 1] && M[i + 1][j] !== undefined) {
        result += M[i + 1][j];
        count += 1;
      }
      // 左下角
      if (M[i - 1] && M[i - 1][j - 1] !== undefined) {
        result += M[i - 1][j - 1];
        count += 1;
      }
      // 下边
      if (M[i] && M[i][j - 1] !== undefined) {
        result += M[i][j - 1];
        count += 1;
      }
      // 右下角
      if (M[i + 1] && M[i + 1][j - 1] !== undefined) {
        result += M[i + 1][j + 1];
        count += 1;
      }
      newM[i].push(Math.floor(result / count));
    }
  }
  return newM;
};

const M = [
  [1, 1, 1],
  [1, 0, 1],
  [1, 1, 1],
];
// [0, 0, 0],
// [0, 0, 0],
// [0, 0, 0],

console.log(imageSmoother(M));
```

`node index.js` 返回：

```js
[0, 0, 0],
[0, 0, 0],
[0, 0, 0],
```

## 四 LeetCode Submit



```js
Accepted
* 202/202 cases passed (224 ms)
* Your runtime beats 12.9 % of javascript submissions
* Your memory usage beats 6.45 % of javascript submissions (44.3 MB)
```

## 五 解题思路



**题倒不难，写起来有点犯晕**。

拿到题目，直接开刷：

```js
const imageSmoother = (M) => {
  const newM = [];
  for(let i = 0; i < M.length; i++) {
    newM[i] = [];
    for (let j = 0; j < M[i].length; j++) {
      let result = 0;
      let count = 0;
      // 左上角
      if (M[i - 1] && M[i - 1][j + 1] !== undefined) {
        result += M[i - 1][j + 1];
        count += 1;
      }
      // 上方
      if (M[i] && M[i][j + 1] !== undefined) {
        result += M[i][j + 1];
        count += 1;
      }
      // 右上角
      if (M[i + 1] && M[i + 1][j + 1] !== undefined) {
        result += M[i + 1][j + 1];
        count += 1;
      }
      // 左边
      if (M[i - 1] && M[i - 1][j] !== undefined) {
        result += M[i - 1][j];
        count += 1;
      }
      // 正中间
      if (M[i] && M[i][j] !== undefined) {
        result += M[i][j];
        count += 1;
      }
      // 右边
      if (M[i + 1] && M[i + 1][j] !== undefined) {
        result += M[i + 1][j];
        count += 1;
      }
      // 左下角
      if (M[i - 1] && M[i - 1][j - 1] !== undefined) {
        result += M[i - 1][j - 1];
        count += 1;
      }
      // 下边
      if (M[i] && M[i][j - 1] !== undefined) {
        result += M[i][j - 1];
        count += 1;
      }
      // 右下角
      if (M[i + 1] && M[i + 1][j - 1] !== undefined) {
        result += M[i + 1][j + 1];
        count += 1;
      }
      newM[i].push(Math.floor(result / count));
    }
  }
  return newM;
};
```

Submit 提交惨不忍睹：

```js
Accepted
* 202/202 cases passed (224 ms)
* Your runtime beats 12.9 % of javascript submissions
* Your memory usage beats 6.45 % of javascript submissions (44.3 MB)
```

代码就不分析了，会看 `if...else...` 的都懂，就是判断每个方位，然后判断每次需要除于的值 `count` 而已。

写完犯晕呼，让我冷静冷静~

如果小伙伴有更好的思路或者方法，欢迎评论留言或者私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

