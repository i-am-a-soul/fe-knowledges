1232 - 缀点成线（check-if-it-is-a-straight-line）
===

> Create by **jsliang** on **2020-02-01 10:49:36**  
> Recently revised in **2020-02-01 11:08:57**

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
* **涉及知识**：几何、数组、数学
* **题目地址**：https://leetcode-cn.com/problems/check-if-it-is-a-straight-line/
* **题目内容**：

在一个 XY 坐标系中有一些点，

我们用数组 coordinates 来分别记录它们的坐标，

其中 coordinates[i] = [x, y] 表示横坐标为 x、纵坐标为 y 的点。

请你来判断，这些点是否在该坐标系中属于同一条直线上，是则返回 true，否则请返回 false。

---

示例 1：

![图](../../../public-repertory/img/other-algorithm-1232-1.jpg)

* 输入：coordinates = [[1,2],[2,3],[3,4],[4,5],[5,6],[6,7]]
* 输出：true

---

示例 2：

![图](../../../public-repertory/img/other-algorithm-1232-2.jpg)

* 输入：coordinates = [[1,1],[2,2],[3,4],[4,5],[5,6],[7,7]]
* 输出：false

提示：

1. 2 <= coordinates.length <= 1000
2. coordinates[i].length == 2
3. -10^4 <= coordinates[i][0], coordinates[i][1] <= 10^4
4. coordinates 中不含重复的点

* 来源：力扣（LeetCode）
* 链接：https://leetcode-cn.com/problems/check-if-it-is-a-straight-line
* 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[][]} coordinates
 * @return {boolean}
 */
var checkStraightLine = function(coordinates) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 缀点成线
 * @param {number[][]} coordinates
 * @return {boolean}
 */
const checkStraightLine = (coordinates) => {
  let count = 0;
  let k = (coordinates[1][1] - coordinates[0][1]) / (coordinates[1][0] - coordinates[0][0]);
  coordinates.forEach((item) => {
    let k2 = (item[1] - coordinates[0][1]) / (item[0] - coordinates[0][0]);
    if (k2 === k || isNaN(k2)) {
      count++;
    }
  });
  return (count === coordinates.length);
};

console.log(checkStraightLine([
  [1, 2],
  [2, 3],
  [3, 4],
  [4, 5],
  [5, 6],
  [6, 7]
])); // true
```

`node index.js` 返回：

```js
true
```

## 四 LeetCode Submit



```js
Accepted
* 66/66 cases passed (64 ms)
* Your runtime beats 80.2 % of javascript submissions
* Your memory usage beats 52.05 % of javascript submissions (34.2 MB)
```

## 五 解题思路



一般数学题，基本上就是套公式，就好比这道题，就是要求这几个点是否在同一条直线上。

然后找到公式就是一顿操作，最后输出结果。

但是想想我找公式还不如认认真真和大佬学：

> 求斜率

```js
const checkStraightLine = (coordinates) => {
  let count = 0;
  let k = (coordinates[1][1] - coordinates[0][1]) / (coordinates[1][0] - coordinates[0][0]);
  coordinates.forEach((item) => {
    let k2 = (item[1] - coordinates[0][1]) / (item[0] - coordinates[0][0]);
    if (k2 === k || isNaN(k2)) {
      count++;
    }
  });
  return (count === coordinates.length);
};
```

Submit 提交为：

```js
Accepted
* 66/66 cases passed (64 ms)
* Your runtime beats 80.2 % of javascript submissions
* Your memory usage beats 52.05 % of javascript submissions (34.2 MB)
```

enm...感觉，又水了一道题，好不嗨皮。

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

