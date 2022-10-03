1030 - 距离顺序排列矩阵单元格（matrix-cells-in-distance-order）
===

> Create by **jsliang** on **2020-01-30 13:59:04**  
> Recently revised in **2020-01-30 14:23:44**

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
* **涉及知识**：排序
* **题目地址**：https://leetcode-cn.com/problems/matrix-cells-in-distance-order/
* **题目内容**：

```
给出 R 行 C 列的矩阵，
其中的单元格的整数坐标为 (r, c)，
满足 0 <= r < R 且 0 <= c < C。

另外，我们在该矩阵中给出了一个坐标为 (r0, c0) 的单元格。

返回矩阵中的所有单元格的坐标，
并按到 (r0, c0) 的距离从最小到最大的顺序排，
其中，两单元格(r1, c1) 和 (r2, c2) 之间的距离是曼哈顿距离，
|r1 - r2| + |c1 - c2|。

（你可以按任何满足此条件的顺序返回答案。）

示例 1：

输入：R = 1, C = 2, r0 = 0, c0 = 0
输出：[[0,0],[0,1]]
解释：从 (r0, c0) 到其他单元格的距离为：[0,1]

示例 2：

输入：R = 2, C = 2, r0 = 0, c0 = 1
输出：[[0,1],[0,0],[1,1],[1,0]]
解释：从 (r0, c0) 到其他单元格的距离为：[0,1,1,2]
[[0,1],[1,1],[0,0],[1,0]] 也会被视作正确答案。

示例 3：

输入：R = 2, C = 3, r0 = 1, c0 = 2
输出：[[1,2],[0,2],[1,1],[0,1],[1,0],[0,0]]
解释：从 (r0, c0) 到其他单元格的距离为：[0,1,1,2,2,3]
其他满足题目要求的答案也会被视为正确，
例如 [[1,2],[1,1],[0,2],[1,0],[0,1],[0,0]]。

提示：

1 <= R <= 100
1 <= C <= 100
0 <= r0 < R
0 <= c0 < C

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/matrix-cells-in-distance-order
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} R
 * @param {number} C
 * @param {number} r0
 * @param {number} c0
 * @return {number[][]}
 */
var allCellsDistOrder = function(R, C, r0, c0) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 距离顺序排列矩阵单元格
 * @param {number} R
 * @param {number} C
 * @param {number} r0
 * @param {number} c0
 * @return {number[][]}
 */
const allCellsDistOrder = (R, C, r0, c0) => {
  const result = [];
  for (let i = 0; i < R; i++) {
    for (let j = 0; j < C; j++) {
      result.push([i, j]);
    }
  }
  result.sort((a, b) => (Math.abs(a[0] - r0) + Math.abs(a[1] - c0)) - (Math.abs(b[0] - r0) + Math.abs(b[1] - c0)))
  return result;
};

console.log(allCellsDistOrder(1, 2, 0, 0)); // [[0, 0], [0, 1]]
console.log(allCellsDistOrder(2, 2, 0, 1)); // [[0, 1], [0, 0], [1, 1], [1, 0]]
```

`node index.js` 返回：

```js
[ [ 0, 0 ], [ 0, 1 ] ]
[ [ 0, 1 ], [ 0, 0 ], [ 1, 1 ], [ 1, 0 ] ]
```

## 四 LeetCode Submit



```js
Accepted
* 66/66 cases passed (188 ms)
* Your runtime beats 75.9 % of javascript submissions
* Your memory usage beats 41.27 % of javascript submissions (49.6 MB)
```

## 五 解题思路



敌人越是强大，你就越要坚强，战胜恐惧的方法就是面对恐惧，加油，奥利给~

咳咳，这道题其实没那么难：

> 暴力破解

```js
const allCellsDistOrder = (R, C, r0, c0) => {
  const result = [];
  for (let i = 0; i < R; i++) {
    for (let j = 0; j < C; j++) {
      result.push([i, j]);
    }
  }
  result.sort((a, b) => (Math.abs(a[0] - r0) + Math.abs(a[1] - c0)) - (Math.abs(b[0] - r0) + Math.abs(b[1] - c0)))
  return result;
};
```

思路嘛：

1. 先做成矩阵 `result`，双重 `for` 循环来个小菜鸡应该都会写。
2. 将 `result` 重新排序，按照题目给出的公式：`|r1 - r2| + |c1 - c2|`，老老实实排序就行了。

Submit 提交：

```js
Accepted
* 66/66 cases passed (188 ms)
* Your runtime beats 75.9 % of javascript submissions
* Your memory usage beats 41.27 % of javascript submissions (49.6 MB)
```

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

