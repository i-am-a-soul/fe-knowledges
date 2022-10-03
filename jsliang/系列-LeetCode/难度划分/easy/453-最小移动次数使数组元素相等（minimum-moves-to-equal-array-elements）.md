453 - 最小移动次数使数组元素相等（minimum-moves-to-equal-array-elements）
===

> Create by **jsliang** on **2019-07-30 09:44:22**  
> Recently revised in **2019-09-18 14:10:23**

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



* **难度**：简单
* **涉及知识**：数学
* **题目地址**：https://leetcode-cn.com/problems/minimum-moves-to-equal-array-elements/
* **题目内容**：

```
给定一个长度为 n 的非空整数数组，找到让数组所有元素相等的最小移动次数。每次移动可以使 n - 1 个元素增加 1。

示例:

输入:
[1,2,3]

输出:
3

解释:
只需要3次移动（注意每次移动会增加两个元素的值）：

[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var minMoves = function(nums) {
  let min =  Math.min.apply(null, nums);
  let count = 0;
  for (let i = 0; i < nums.length; i++) {
    count += nums[i] - min;
  }
  return count;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



1. `nums`：`[1,2,3]`
2. `return`：

```js
3
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
✔ Accepted
  ✔ 84/84 cases passed (92 ms)
  ✔ Your runtime beats 87.39 % of javascript submissions
  ✔ Your memory usage beats 68.42 % of javascript submissions (37.3 MB)
```

## <a name="chapter-six" id="chapter-six">六 知识点</a>



1. `Math`：JS 中的内置对象，具有数学常数和函数的属性和方法。[`Math` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Math/README.md)

## <a name="chapter-seven" id="chapter-seven">七 解题思路</a>



**首先**，拿到这道题，不要一脸懵逼，理解下题目中的移动，再尝试更多的移动：

> 案例

```js
[1,2,3] =>
[2,3,3] =>
[3,4,3] =>
[4,4,4]
```

> 尝试 1

```js
[1,3,4] =>
[2,4,4] =>
[3,5,4] =>
[4,5,5] =>
[5,6,5] =>
[6,6,6]
```

> 尝试 2

```js
[1,3,5] =>
[2,4,5] =>
[3,5,5] =>
[4,6,5] =>
[5,6,6] =>
[6,7,6] =>
[7,7,7]
```

> 尝试 3

```js
[2,4,6,8] =>
[3,5,7,8] =>
[4,6,8,8] =>
[5,7,9,8] =>
[6,8,9,9] =>
[7,9,10,9] =>
[8,10,10,10] =>
[9,11,11,10] =>
[10,12,11,11] =>
[11,12,12,12] =>
[12,13,13,12] =>
[13,14,13,13] =>
[14,14,14,14] =>
```

尝试发现规律：**移动次数等于所有值减去最小值**。

例如：

1. 案例移动了 3 次，为：(3 - 1) + (2 - 1)
2. 尝试 1 移动了 5 次，为：(4 - 1) + (3 - 1)
3. 尝试 2 移动了 6 次，为：(5 - 1) + (3 - 1）
4. 尝试 3 移动了 12 次，为：(8 - 2) + (6 - 2) + (4 - 2)

**然后**，见证奇迹的时刻到了：

```js
var minMoves = function(nums) {
  let min =  Math.min.apply(null, nums);
  let count = 0;
  for (let i = 0; i < nums.length; i++) {
    count += nums[i] - min;
  }
  return count;
};
```

Submit 提交后：

```js
✔ Accepted
  ✔ 84/84 cases passed (92 ms)
  ✔ Your runtime beats 87.39 % of javascript submissions
  ✔ Your memory usage beats 68.42 % of javascript submissions (37.3 MB)
```

**最后**，得出结论：丫的就一找规律题~

> 大佬优化的代码：

```js
var minMoves = function (nums) {
  var min = Math.min(...nums);
  return nums.map(function (a) {
    return a - min;
  }).reduce(function (a, b) {
    return a + b;
  })
};
```

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

