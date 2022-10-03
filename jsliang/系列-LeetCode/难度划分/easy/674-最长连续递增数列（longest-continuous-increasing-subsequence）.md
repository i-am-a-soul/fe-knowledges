674 - 最长连续递增数列（longest-continuous-increasing-subsequence）
===

> Create by **jsliang** on **2019-12-11 07:49:26**  
> Recently revised in **2019-12-11 08:41:16**

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
* **题目地址**：https://leetcode-cn.com/problems/longest-continuous-increasing-subsequence/
* **题目内容**：

```
给定一个未经排序的整数数组，找到最长且连续的的递增序列。

示例 1:

输入: [1,3,5,4,7]
输出: 3
解释: 
最长连续递增序列是 [1,3,5]，长度为 3。
尽管 [1,3,5,7] 也是升序的子序列, 
但它不是连续的，因为5和7在原数组里被 4 隔开。 

示例 2:

输入: [2,2,2,2,2]
输出: 1
解释: 最长连续递增序列是 [2], 长度为1。
注意：数组长度不会超过10000。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findLengthOfLCIS = function(nums) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 最长连续递增序列
 * @param {number[]} nums
 * @return {number}
 */
const findLengthOfLCIS = (nums) => {
  let result = [nums[0]];
  for (let i = 0; i < nums.length; i++) {
    if (nums[i + 1] > nums[i]) {
      const temp = [];
      for (let j = i; j < nums.length; j++) {
        temp.push(nums[j]);
        if (nums[j + 1] <= nums[j]) {
          break;
        }
      }
      if (temp.length > result.length) {
        result = temp;
      }
    }
  }
  console.log(result);
  return result.length;
};

// console.log(findLengthOfLCIS([1, 3, 5, 4, 7])); // 3
console.log(findLengthOfLCIS([])); // 0
```

`node index.js` 返回：

```js
0
```

## 四 LeetCode Submit



```js
Accepted
* 36/36 cases passed (76 ms)
* Your runtime beats 40.74 % of javascript submissions
* Your memory usage beats 5.16 % of javascript submissions (42.1 MB)
```

## 五 解题思路



**最初的灵感，往往是脑子一抽，代码就出来了。**

> 暴力破解

```js
const findLengthOfLCIS = (nums) => {
  let result = nums[0] ? [nums[0]] : [];
  for (let i = 0; i < nums.length; i++) {
    if (nums[i + 1] > nums[i]) {
      const temp = [];
      for (let j = i; j < nums.length; j++) {
        temp.push(nums[j]);
        if (nums[j + 1] <= nums[j]) {
          break;
        }
      }
      if (temp.length > result.length) {
        result = temp;
      }
    }
  }
  return result.length;
};
```

思路很简单：

1. 设置 `result`，它的判断是为了防止 `[2, 2, 2, 2, 2]` 和 `[]` 的情况，这两种情况中，一个是长度为 1，一个是长度为 0。
2. 通过 `for` 遍历数组，如果下一个元素比当前元素大，那么破案的时候到了。
3. 设置 `temp` 记录这个 “最长连续递增数列”，通过 `for` 遍历剩下的数组，每次往 `temp` 中 `push` 新元素，直到下一个元素小于或者等于当前元素，则中止循环。
4. 判断 `temp` 的长度和 `result` 的长度，如果 `temp` 比较长，那么重置 `result`。
5. 最终返回 `result` 的长度。

Submit 提交：

```js
Accepted
* 36/36 cases passed (76 ms)
* Your runtime beats 40.74 % of javascript submissions
* Your memory usage beats 5.16 % of javascript submissions (42.1 MB)
```

## 六 进一步思考



参考了下【题解区】官网的解法，学到了一种新解法：

* **滑动窗口**

```js
const findLengthOfLCIS = (nums) => {
  let result = 0,
      position = 0;
  for (let i = 0; i < nums.length; i++) {
    if (i > 0 && nums[i] < nums[i - 1]) {
      position = i;
    }
    result = Math.max(result, i - position + 1);
  }
  return result;
};
```

Submit 提交：

```js
Accepted
* 36/36 cases passed (64 ms)
* Your runtime beats 82.87 % of javascript submissions
* Your memory usage beats 20.62 % of javascript submissions (35.5 MB)
```

咱们先讲下这道题的思路，然后初步探索下滑动窗口：

1. 设置 `result` 为结果值，`position` 用来记录位置。
2. 遍历 `nums`，从第二个开始（`i > 0`），将当前值和前一个值和前一个值比较（`nums[i] < nums[i - 1]`），如果当前值小于前一个值，说明这个连续长度中断了（不是递增的了）。设置 `position` 为 `i`。
3. 每次我们都将 `result` 和 `i - position + 1` 比较，`i - position + 1` 就是这个连续递增持续到现在的长度。
4. 最终返回 `result` 即可。

为什么说它好呢？

1. 它只用了一次遍历，而我们的暴力用了双重嵌套 `for`。
2. 它使用了常数空间，而我们的暴力用了数组空间。

那么，什么是滑动窗口？它解决了什么问题？

滑动问题包含一个滑动窗口，它是一个运行在一个大数组上的子列表，该数组是一个底层元素集合。

滑动窗口算法可以将嵌套的循环问题，转换为单循环问题，降低时间复杂度。

很恰巧，翻到一个感觉不错的链接，知乎的：

* 什么是「滑动窗口算法」（sliding window algorithm），有哪些应用场景？https://www.zhihu.com/question/314669016

它就滑动窗口作出了 JavaScript 的解释，咱们看其中一个问题：

...无法复制，小伙伴们可以自行前往查看~

改天咱们到算法模块专门讲解，持续关注公众号或者点击公众号原文关注我的仓库咯~

https://github.com/LiangJunrong/document-library/blob/master/other-library/LeetCode/algorithms-and-data-structures/%E7%AE%97%E6%B3%95-%E6%A8%A1%E5%BC%8F-%E6%BB%91%E5%8A%A8%E7%AA%97%E5%8F%A3.md

那么，今天到此结束，明儿见！

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

