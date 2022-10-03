836 - 矩形重叠（rectangle-overlap）
===

> Create by **jsliang** on **2020-01-08 19:22:41**  
> Recently revised in **2020-1-8 22:55:08**

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
* **题目地址**：https://leetcode-cn.com/problems/rectangle-overlap/
* **题目内容**：

```
矩形以列表 [x1, y1, x2, y2] 的形式表示，
其中 (x1, y1) 为左下角的坐标，(x2, y2) 是右上角的坐标。

如果相交的面积为正，
则称两矩形重叠。
需要明确的是，
只在角或边接触的两个矩形不构成重叠。

给出两个矩形，判断它们是否重叠并返回结果。

示例 1：

输入：rec1 = [0,0,2,2], rec2 = [1,1,3,3]
输出：true
示例 2：

输入：rec1 = [0,0,1,1], rec2 = [1,0,2,1]
输出：false
说明：

两个矩形 rec1 和 rec2 都以含有四个整数的列表的形式给出。
矩形中的所有坐标都处于 -10^9 和 10^9 之间。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} rec1
 * @param {number[]} rec2
 * @return {boolean}
 */
var isRectangleOverlap = function(rec1, rec2) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 矩形重叠
 * @param {number[]} rec1
 * @param {number[]} rec2
 * @return {boolean}
 */
const isRectangleOverlap = (rec1, rec2) => {
  return !(
    rec1[2] <= rec2[0]      // left
    || rec1[3] <= rec2[1]   // bottom
    || rec1[0] >= rec2[2]   // right
    || rec1[1] >= rec2[3]   // top
  );
};

console.log(isRectangleOverlap([0, 0, 2, 2], [1, 1, 3, 3])); // true
// rec1: [[0, 0], [2, 0], [2, 2], [0, 2]]
// rec2: [[1, 1], [3, 1], [3, 3], [1, 3]]

console.log(isRectangleOverlap([0, 0, 1, 1], [1, 0, 2, 1])); // false
// rec1: [[0, 0], [1, 0], [1, 1], [0, 1]]
// rec2: [[1, 0], [2, 0], [2, 1], [1, 2]]

console.log(isRectangleOverlap([8, 20, 12, 20], [14, 2, 19, 11])); // false
// rec1: [[8, 20], [12, 20]] —— 不能构成矩形！

console.log(isRectangleOverlap([5, 15, 8, 18], [0, 3, 7, 9])); // false
// rec1: [[5, 15], [8, 15], [8, 18], [5, 18]]
// rec2: [[0, 3], [7, 3], [7, 9], [0, 9]]
```

`node index.js` 返回：

```js
true
false
false
false
```

## 四 LeetCode Submit



```js
Accepted
* 43/43 cases passed (64 ms)
* Your runtime beats 50 % of javascript submissions
* Your memory usage beats 13.33 % of javascript submissions (33.7 MB)
```

## 五 解题思路



拿到题目，一看坐标轴，脑海要二维画图 —— 瞎猜吧：

> 错误题解 - 失败的各种实验

```js
const isRectangleOverlap = (rec1, rec2) => {
  // 不能构成矩形，纵坐标相等
  if (rec1[1] === rec1[3] || rec2[1] === rec2[3]) {
    return false;
  }
  // x1, y1 === 左下角
  // x3, y1 === 右下角
  // x3, y3 === 右上角
  // x1, y3 === 左上角
  const fullRec1 = [rec1[0], rec1[1], rec1[2], rec1[1], rec1[2], rec1[3], rec1[0], rec1[3]].sort((a, b) => a - b);
  const fullRec2 = [rec2[0], rec2[1], rec2[2], rec2[1], rec2[2], rec2[3], rec2[0], rec2[3]].sort((a, b) => a - b);
  const fullRec1Min = fullRec1[0],
        fullRec1Max = fullRec1[fullRec1.length - 1],
        fullRec2Min = fullRec2[0],
        fullRec2Max = fullRec2[fullRec2.length - 1];
  let count = 0;
  console.log('------');
  console.log(fullRec1);
  console.log(fullRec2);
  if (fullRec1Max < fullRec2Max) {
    for (let i = 0; i < fullRec2.length; i++) {
      if (fullRec2[i] >= fullRec1Min && fullRec2[i] < fullRec1Max) {
        count ++;
      }
    }
  } else {
    for (let i = 0; i < fullRec1.length; i++) {
      if (fullRec1[i] >= fullRec2Min && fullRec1[i] < fullRec2Max) {
        count ++;
      }
    }
  }
  return count >= 4;
};

console.log(isRectangleOverlap([0, 0, 2, 2], [1, 1, 3, 3])); // true
// rec1: [[0, 0], [2, 0], [2, 2], [0, 2]]
// rec2: [[1, 1], [3, 1], [3, 3], [1, 3]]

console.log(isRectangleOverlap([0, 0, 1, 1], [1, 0, 2, 1])); // false
// rec1: [[0, 0], [1, 0], [1, 1], [0, 1]]
// rec2: [[1, 0], [2, 0], [2, 1], [1, 2]]

console.log(isRectangleOverlap([8, 20, 12, 20], [14, 2, 19, 11])); // false
// rec1: [[8, 20], [12, 20]] —— 不能构成矩形！

console.log(isRectangleOverlap([5, 15, 8, 18], [0, 3, 7, 9])); // false
// rec1: [[5, 15], [8, 15], [8, 18], [5, 18]]
// rec2: [[0, 3], [7, 3], [7, 9], [0, 9]]
```

想着确认两个矩形的 4 个点，然后求证其中一个矩形在另一个矩形的点有 4 个以上，即为重叠，结果惨败滑铁卢：

```js
Wrong Answer
32/43 cases passed (N/A)

Testcase
[5,15,8,18]
[0,3,7,9]

Answer
true

Expected Answer
false
```

看了下它的点：

```js
console.log(isRectangleOverlap([5, 15, 8, 18], [0, 3, 7, 9])); // false
// rec1: [[5, 15], [8, 15], [8, 18], [5, 18]]
// rec2: [[0, 3], [7, 3], [7, 9], [0, 9]]
```

它是刚好有 4 个的，但是却是不符合了，所以这方法也得舍弃掉~

## 六 进一步思考



所谓进一步思考，只能看看官方思路了，毕竟真不会，压根没想到这种题目：

* 官方题解：https://leetcode-cn.com/problems/rectangle-overlap/solution/ju-zhen-zhong-die-by-leetcode/

> 解法一：检查位置

```js
const isRectangleOverlap = (rec1, rec2) => {
  return !(
    rec1[2] <= rec2[0]      // left
    || rec1[3] <= rec2[1]   // bottom
    || rec1[0] >= rec2[2]   // right
    || rec1[1] >= rec2[3]   // top
  );
};
```

一个很简单的法子，判断 `rec1` 是否高于、低于或者在 `rec2` 左右两侧。

小伙伴可以拿纸笔画出来试试看~

> 解法二：检查区域

```js
const isRectangleOverlap = (rec1, rec2) => {
  return (
    Math.min(rec1[2], rec2[2]) > Math.max(rec1[0], rec2[0])     // width > 0
    && Math.min(rec1[3], rec2[3]) > Math.max(rec1[1], rec2[1])  // height > 0
  );
};
```

看完代码心肌梗塞的感觉……

好心累……（被狂虐）

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

