1037 - 有效的回旋镖（valid-boomerang）
===

> Create by **jsliang** on **2020-01-30 16:21:42**  
> Recently revised in **2020-01-30 16:54:38**

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
* **题目地址**：https://leetcode-cn.com/problems/valid-boomerang/
* **题目内容**：

```
回旋镖定义为一组三个点，这些点各不相同且不在一条直线上。

给出平面上三个点组成的列表，判断这些点是否可以构成回旋镖。

示例 1：

输入：[[1,1],[2,3],[3,2]]
输出：true

示例 2：

输入：[[1,1],[2,2],[3,3]]
输出：false

提示：

points.length == 3
points[i].length == 2
0 <= points[i][j] <= 100

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/valid-boomerang
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[][]} points
 * @return {boolean}
 */
var isBoomerang = function(points) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 有效的回旋镖
 * @param {number[][]} points
 * @return {boolean}
 */
const isBoomerang = (points) => {
  const Ax = points[0][0];
  const Ay = points[0][1];
  const Bx = points[1][0];
  const By = points[1][1];
  const Cx = points[2][0];
  const Cy = points[2][1];
  return (Ax * (By - Cy) + Bx * (Cy - Ay) + Cx * (Ay - By)) / 2 !== 0;
};

console.log(isBoomerang([[1, 1], [2, 3], [3, 2]])); // true
```

`node index.js` 返回：

```js
true
```

## 四 LeetCode Submit



```js
Accepted
* 190/190 cases passed (60 ms)
* Your runtime beats 93.1 % of javascript submissions
* Your memory usage beats 38.78 % of javascript submissions (33.8 MB)
```

## 五 解题思路



元芳，这道题你怎么看？

大人！我不知道这道题数学公式！

是的，坑爹的，又要百度搜索公式了：

* 判断三个点是否构成三角形公式：(Ax * (By - Cy) + Bx * (Cy - Ay) + Cx * (Ay - By)) / 2 !== 0

> 暴力破解

```js
const isBoomerang = (points) => {
  const Ax = points[0][0];
  const Ay = points[0][1];
  const Bx = points[1][0];
  const By = points[1][1];
  const Cx = points[2][0];
  const Cy = points[2][1];
  return (Ax * (By - Cy) + Bx * (Cy - Ay) + Cx * (Ay - By)) / 2 !== 0;
};
```

直接套用公式就行了，Submit 提交：

```js
Accepted
* 190/190 cases passed (60 ms)
* Your runtime beats 93.1 % of javascript submissions
* Your memory usage beats 38.78 % of javascript submissions (33.8 MB)
```

那些说只需要一行的给我站住，看我不兜晕你：

> 一行求解

```js
const isBoomerang = (points) => (points[0][0] * (points[1][1] - points[2][1]) + points[1][0] * (points[2][1] - points[0][1]) + points[2][0] * (points[0][1] - points[1][1])) / 2 !== 0;
```

Submit 提交：

```js
Accepted
* 190/190 cases passed (64 ms)
* Your runtime beats 77.59 % of javascript submissions
* Your memory usage beats 97.96 % of javascript submissions (33.5 MB)
```

## 六 进一步思考



肯定还有的小伙伴说会有更简单的公式：

> 暴力破解【简化】

```js
/**
 * @name 有效的回旋镖
 * @param {number[][]} points
 * @return {boolean}
 */
const isBoomerang = (points) => {
  const dx = points[1][0] - points[0][0];
  const dy = points[1][1] - points[0][1];
  const ex = points[2][0] - points[0][0];
  const ey = points[2][1] - points[0][1];
  return dx * ey != ex * dy;
}
```

Submit 提交：

```js
Accepted
* 190/190 cases passed (60 ms)
* Your runtime beats 93.1 % of javascript submissions
* Your memory usage beats 97.96 % of javascript submissions (33.5 MB)
```

就酱，这道题就结束啦！

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

