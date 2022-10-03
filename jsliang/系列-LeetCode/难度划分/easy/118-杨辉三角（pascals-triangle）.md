118 - 杨辉三角（pascals-triangle）
===

> Create by **jsliang** on **2019-6-27 07:33:45**  
> Recently revised in **2019-09-18 10:25:04**

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
| [八 进一步探索](#chapter-eight) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/pascals-triangle/
* **题目内容**：

```
给定一个非负整数 numRows，生成杨辉三角的前 numRows 行。

在杨辉三角中，每个数是它左上方和右上方的数的和。

示例:

输入: 5
输出:
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

* **解题代码**：

```js
var generate = function(numRows) {
  if (numRows === 0) {
    return []
  }
  if (numRows === 1) {
    return [[1]];
  }
  let fullResult = [
    [1],
    [1, 1],
  ];
  let recursion = function(numRows) {
    if (numRows === 2) {
      return fullResult[1];
    }
    let prevArr = recursion(numRows - 1);
    let result = [];
    for (let i = 0; i < prevArr.length; i++) {
      if (prevArr[i] && prevArr[i + 1]) {
        result.push(prevArr[i] + prevArr[i + 1]);
      }
    }
    result = [1, ...result, 1];
    fullResult.push(result);
    return result;
  }
  recursion(numRows);
  return fullResult;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



1. `numRows`：`5`
2. `return`：

```js
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
√ Accepted
  √ 15/15 cases passed (76 ms)
  √ Your runtime beats 87.82 % of javascript submissions
  √ Your memory usage beats 11.38 % of javascript submissions (34 MB)
```

## <a name="chapter-six" id="chapter-six">六 知识点</a>



`push()`：`push()` 方法将一个或多个元素添加到数组的末尾，并返回该数组的新长度。[`push()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Array/push.md)

## <a name="chapter-seven" id="chapter-seven">七 解题思路</a>



**天才第一步，梁氏破解路**

当然是选择最简单粗暴的暴力破解啦：

```js
var generate = function(numRows) {
  switch (numRows) {
    case 0:
      return [];
    case 1:
      return [
        [1]
      ];
    case 2:
      return [
        [1],
        [1, 1]
      ];
    case 3:
      return [
        [1],
        [1, 1],
        [1, 2, 1],
      ];
    case 4:
      return [
        [1],
        [1, 1],
        [1, 2, 1],
        [1, 3, 3, 1],
      ];
    case 5:
      return [
        [1],
        [1, 1],
        [1, 2, 1],
        [1, 3, 3, 1],
        [1, 4, 6, 4, 1],
      ];
    // case 6……
  }
};
```

开玩笑开玩笑~

不过，只有 15 个测试用例，暴力破解应该是最快的，哈哈。

回归正题，还是使用正常的暴力破解解题思路（卧槽，不还是暴力破解）：

**首先**，观察多几遍题意：

```js
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

就是说，我左边的 1 和右边的 1，是固定不动的，即：

`[1, ..., 1]`

**然后**，看到上面，我们应该明白，我们只需要把中间的和求出来，直接通过 ES6 的扩展运算符插入数组进去，就可以获取到第 `numRows` 行的代码：

`[1, ...prevResult, 1]`

**最后**，就是求出 `prevResult`。

所以还是使用递归吧，在 `numRows` 为 2 的时候，返回 `[1, 1]`，遍历一遍结果为 `[2]`，塞到数组中即为：`[1, 2, 1]`，以此类推：

* `numsRows === 3`：`[1, 2, 1]`
* `numsRows === 4`：`[1, 3, 3, 1]`
* ……

这样，我们就完成了暴力破解的解法啦~

> 感觉 **jsliang** 还是念念不忘 `switch...case...`，感觉是最优解有木有！

## <a name="chapter-eight" id="chapter-eight">八 进一步探索</a>



**jsliang** 目前的习惯就是：

如果自己做出来了，那就看看别人的思路，兴许会眼前一亮呢……

可惜的是这一次还真没有，看起来也没简洁到哪去。

不过还是贴上来吧，我也就不讲解啦：

> 攻略 1

```js
var generate = function(numRows) {
  // 规律 a[i][j] = a[i-2][j-1]+a[i-2][j]
  let arr = [];
  if (numRows == 0) {
    return arr;
  }
  for (let i = 1; i < numRows + 1; i++) {
    var temp = [];
    for (let j = 0; j < i; j++) {
      if (j == 0 || j == i - 1) {
        temp.push(1);
      } else {
        temp.push(arr[i - 2][j - 1] + arr[i - 2][j]);
      }
    }
    arr.push(temp);
  }
  return arr;
};
```

通过 `for` 遍历求出每层的值，再添加到 `arr` 中。

> 攻略 2

```js
var generate = function(numRows) {
  const res = [];
  for (let i = 0; i < numRows; i++) {
    if (i === 0) {
      res.push([1]); // 第一行 基础行
    } else {
      const arrs = [1]; // 初始化当前行的第一个元素为1
      const preRows = res[i - 1]; // 上一行数据
      for (let j = 0; j < preRows.length; j++) {
        // 上一行遍历获取左上方和右上方的数的和
        arrs.push(preRows[j] + (preRows[j + 1] || 0));
      }
      res.push(arrs);
    }
  }
  return res;
};
```

比攻略 1 优秀点，可以吸取下经验。

那么，本题就此结束啦~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

