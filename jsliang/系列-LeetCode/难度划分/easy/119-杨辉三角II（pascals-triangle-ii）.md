119 - 杨辉三角II（pascals-triangle-ii）
===

> Create by **jsliang** on **2019-6-28 07:39:47**  
> Recently revised in **2019-09-18 10:25:46**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| &emsp;[3.1 解法 - 常规解法](#chapter-three-one) |
| &emsp;[3.2 解法 - 数学解法](#chapter-three-two) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/pascals-triangle-ii/
* **题目内容**：

```
给定一个非负索引 k，其中 k ≤ 33，返回杨辉三角的第 k 行。

在杨辉三角中，每个数是它左上方和右上方的数的和。

示例:

输入: 3
输出: [1,3,3,1]
进阶：

你可以优化你的算法到 O(k) 空间复杂度吗？
```

> 补充：杨辉三角类似于：

```js
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

### <a name="chapter-three-one" id="chapter-three-one">3.1 解法 - 常规解法</a>



* **解题代码**：

```js
var getRow = function(rowIndex) {
  if (!rowIndex) {
    return [1];
  }
  if (rowIndex === 1) {
    return [1, 1];
  }
  let recursion = getRow(rowIndex - 1);
  let result = [];
  for (let i = 0; i < rowIndex; i++) {
    if (recursion[i] && recursion[i + 1]) {
      result.push(recursion[i] + recursion[i + 1]);
    }
  }
  return [1, ...result, 1];
};
```

* **执行测试**：

1. `rowIndex`：`5`
2. `return`：

```js
[ 1, 5, 10, 10, 5, 1 ]
```

* **LeetCode Submit**：

```js
√ Accepted
  √ 34/34 cases passed (80 ms)
  √ Your runtime beats 83.43 % of javascript submissions
  √ Your memory usage beats 7.19 % of javascript submissions (35.1 MB)
```

* **知识点**：

`push()`：`push()` 方法将一个或多个元素添加到数组的末尾，并返回该数组的新长度。[`push()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Array/push.md)

* **解题思路**：

**首先**，今天一大早起来看到这道题，瞪，第一感觉是我昨天是不是做了什么了不得的事儿……

昨天的题也是杨辉三角（题 118），传递一个参数 n，获取它的 n 行记录，即：

```js
if (n === 4) {
  return [
    [1],
    [1, 1],
    [1, 2, 1],
    [1, 3, 3, 1],
  ]
}
```

**然后**，昨天我的做法就是：统计每行的返回结果，最终汇总到一块。

所以……

我昨天就破解了两道题了啊-_-||

**最后**，还是扯下思路吧：

* 如果 `rowIndex` 为 `0`，返回 `[1]`
* 如果 `rowIndex` 为 `1`，返回 `[1, 1]`
* 递归 `getRow(rowIndex - 1)`，然后求出中间的和，并 `return` 出来 `[1, ...result, 1]`

细节小伙伴们可以打印看看是怎么一回事，在此就不多累述了。

### <a name="chapter-three-two" id="chapter-three-two">3.2 解法 - 数学解法</a>



* **解题代码**：

```js
var getRow = function(rowIndex) {
  let a = 1;
  let arr = [];
  for (let i = 0; i <= rowIndex; i++) {
    arr.push(a);
    a = (a * (rowIndex - i)) / (i + 1);
  }
  return arr;
};
```

* **执行测试**：

1. `5`
2. `return`：

```js
[ 1, 5, 10, 10, 5, 1 ]
```

* **LeetCode Submit**：

```js
√ Accepted
  √ 34/34 cases passed (72 ms)
  √ Your runtime beats 94.57 % of javascript submissions
  √ Your memory usage beats 62.09 % of javascript submissions (33.7 MB)
```

* **知识点**：

`push()`：`push()` 方法将一个或多个元素添加到数组的末尾，并返回该数组的新长度。[`push()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Array/push.md)

* **解题思路**：

惯例看下 LeetCode 解题库：

大佬受我一拜！

初瞄，感觉是数学解法，卧槽，数学大佬，是不是小学获得过奥林匹克数学竞赛奖的~

我不管，我没看懂，我不解释，等小伙伴们给我留言评论，说出这种解法思路的第一个小伙伴，获取赏金 6.66！

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

