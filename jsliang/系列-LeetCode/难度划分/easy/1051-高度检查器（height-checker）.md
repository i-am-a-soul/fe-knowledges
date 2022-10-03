1051 - 高度检查器（height-checker）
===

> Create by **jsliang** on **2020-01-30 22:21:36**  
> Recently revised in **2020-01-30 22:45:09**

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
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/height-checker/
* **题目内容**：

```
学校在拍年度纪念照时，
一般要求学生按照 非递减 的高度顺序排列。

请你返回能让所有学生以 非递减 高度排列的最小必要移动人数。

示例：

输入：heights = [1,1,4,2,1,3]
输出：3

提示：

1 <= heights.length <= 100
1 <= heights[i] <= 100

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/height-checker
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} heights
 * @return {number}
 */
var heightChecker = function(heights) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 高度检查器
 * @param {number[]} heights
 * @return {number}
 */
const heightChecker = (heights) => {
  const newHeights = [...heights].sort((a, b) => a - b);
  let people = 0;
  for (let i = 0; i < heights.length; i++) {
    if (heights[i] !== newHeights[i]) {
      people++;
    }
  }
  return people;
};

console.log(heightChecker([1, 1, 4, 2, 1, 3])); // 3
```

`node index.js` 返回：

```js
3
```

## 四 LeetCode Submit



```js
Accepted
* 79/79 cases passed (72 ms)
* Your runtime beats 66.01 % of javascript submissions
* Your memory usage beats 42.98 % of javascript submissions (35.1 MB)
```

## 五 解题思路



题目让我感到困惑：

1. 给定一个数组：`heights = [1, 1, 4, 2, 1, 3]`。
2. 尽可能少的移动，让其变成【非递减】排序。
3. 求出这个最少的移动人数。

按照 **jsliang** 自身的理解，将 4 移动到 3 后面，将 2 移动到 1 后面，总共 2 次移动，搞定收工。

但是，示例返回的是 `3`，这就让我感到困惑无比了~

接着我想了下，它的意思是不是说：`[4, 2, 1]` 移动了位置变成了 `[1, 2,3, 4]`，所以移动次数是 `3`？还是不对啊，皱眉。

再搞搞，意思是：4 和 1 调换，4 再和 3 调换，所以移动了 3 个人？

那样的话……

> 暴力破解

```js
const heightChecker = (heights) => {
  const newHeights = [...heights].sort((a, b) => a - b);
  let people = 0;
  for (let i = 0; i < heights.length; i++) {
    if (heights[i] !== newHeights[i]) {
      people++;
    }
  }
  return people;
};
```

我们将 `height` 进行 `sort()` 的顺序操作，得到递增数列 `newHeight`。

然后逐一比较 `height` 和 `newHeight`，所不同的位置，就是它们需要移动的次数。

Submit 提交：

```js
Accepted
* 79/79 cases passed (72 ms)
* Your runtime beats 66.01 % of javascript submissions
* Your memory usage beats 42.98 % of javascript submissions (35.1 MB)
```

## 六 进一步思考



看下【题解区】发现都是大佬：

> 桶

```js
const heightChecker = (heights) => {
  let arr = [0];
  heights.forEach(h => {
    if (arr[h]) {
      arr[h]++;
    } else {
      arr[h] = 1;
    }
  });
  let count = 0;
  let k = 0;
  arr.forEach((a, i) => {
    while(a--){
      if(heights[k++] !== i) {
        count++;
      }
    }
  })
  return count;
};
```

Submit 提交：

```js
Accepted
* 79/79 cases passed (64 ms)
* Your runtime beats 92.74 % of javascript submissions
* Your memory usage beats 97.52 % of javascript submissions (34.3 MB)
```

唯有先羡慕一番，后面学习了各种排序方法后，再逐一复习~

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

