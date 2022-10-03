566 - 重塑矩阵（reshape-the-matrix）
===

> Create by **jsliang** on **2019-11-18 08:23:14**  
> Recently revised in **2019-11-18 09:06:48**

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
* **题目地址**：https://leetcode-cn.com/problems/reshape-the-matrix/
* **题目内容**：

```
在 MATLAB 中，有一个非常有用的函数 reshape。

它可以将一个矩阵重塑为另一个大小不同的新矩阵，但保留其原始数据。

给出一个由二维数组表示的矩阵，

以及两个正整数 r 和 c，

分别表示想要的重构的矩阵的行数和列数。

重构后的矩阵需要将原始矩阵的所有元素以相同的行遍历顺序填充。

如果具有给定参数的 reshape 操作是可行且合理的，则输出新的重塑矩阵；

否则，输出原始矩阵。

示例 1:

输入: 
nums = 
[[1,2],
 [3,4]]
r = 1, c = 4

输出: 
[[1,2,3,4]]

解释:
行遍历nums的结果是 [1,2,3,4]。新的矩阵是 1 * 4 矩阵, 
用之前的元素值一行一行填充新矩阵。

示例 2:

输入: 
nums = 
[[1,2],
 [3,4]]
r = 2, c = 4

输出: 
[[1,2],
 [3,4]]

解释:
没有办法将 2 * 2 矩阵转化为 2 * 4 矩阵。 所以输出原矩阵。

注意：
给定矩阵的宽和高范围在 [1, 100]。
给定的 r 和 c 都是正数。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[][]} nums
 * @param {number} r
 * @param {number} c
 * @return {number[][]}
 */
var matrixReshape = function(nums, r, c) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 重塑矩阵
 * @param {number[][]} nums
 * @param {number} r
 * @param {number} c
 * @return {number[][]}
 */
const matrixReshape = (nums, r, c) => {
  // 1. 获取二维数组的所有元素的个数，判断其值是否等于 r * c
  const newNums = [].concat.apply([],nums);
  if (newNums.length !== r * c) {
    return nums;
  }
  // 2. 符合转换条件
  const result = [];
  for (let i = 0; i < r; i++) {
    result[i] = newNums.splice(0, c);
  }
  return result;
};

console.log(matrixReshape([[1, 2], [3, 4]], 1, 4)); // [[1, 2, 3, 4]]
```

`node index.js` 返回：

```js
[[1, 2, 3, 4]]
```

## 四 LeetCode Submit



```js
Accepted
* 56/56 cases passed (80 ms)
* Your runtime beats 100 % of javascript submissions
* Your memory usage beats 97.92 % of javascript submissions (39.3 MB)
```

## 五 解题思路



**首先**，审题，刨出关键字：

1. 如果合理，则输出新数组；如果不合理，则保留其原始数据
2. 参数：二维数组、正整数 r（行数）和 c（列数）

如上。

**然后**，尝试按照自己理解解题：

```js
const matrixReshape = (nums, r, c) => {
  // 1. 获取二维数组的所有元素的个数，判断其值是否等于 r * c
  const newNums = [].concat.apply([], nums);
  if (newNums.length !== r * c) {
    return nums;
  }
  // 2. 符合转换条件
  const result = [];
  for (let i = 0; i < r; i++) {
    result[i] = newNums.splice(0, c);
  }
  return result;
};
```

Submit 提交试试：

```js
Accepted
* 56/56 cases passed (80 ms)
* Your runtime beats 100 % of javascript submissions
* Your memory usage beats 97.92 % of javascript submissions (39.3 MB)
```

哇！！这是直接跃升成第一名么，酷~

**最后**，讲讲思路，思路非常简单：

1. 将二维数组平整为一维数组。（通过 `apply` 将二维数组转成一维数组不会影响到原数组）
2. 判断一维数组的长度能否换成 `r * c` 格式，如果不行，那么返回原数组。
3. 如果可以，那么遍历 r 的个数，将 `newNums` 通过 `splice()` 依次切割到对应的位置即可。

看到这里，会不会觉得这道题特别简单！

如果小伙伴们有其他更好的方法或者思路，欢迎评论留言或者私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

