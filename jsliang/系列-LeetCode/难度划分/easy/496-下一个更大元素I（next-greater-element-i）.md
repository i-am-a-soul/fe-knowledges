496 - 下一个更大元素I（next-greater-element-i）
===

> Create by **jsliang** on **2019-10-29 10:40:59**  
> Recently revised in **2019-10-29 20:13:05**

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
* **涉及知识**：栈
* **题目地址**：https://leetcode-cn.com/problems/next-greater-element-i/
* **题目内容**：

```
给定两个没有重复元素的数组 nums1 和 nums2，其中nums1 是 nums2 的子集。

找到 nums1 中每个元素在 nums2 中的下一个比其大的值。

nums1 中数字 x 的下一个更大元素是指：

x 在 nums2 中对应位置的右边的第一个比 x 大的元素。

如果不存在，对应位置输出-1。

示例 1:
输入: nums1 = [4,1,2], nums2 = [1,3,4,2].
输出: [-1,3,-1]
解释:
  对于num1中的数字4，你无法在第二个数组中找到下一个更大的数字，因此输出 -1。
  对于num1中的数字1，第二个数组中数字1右边的下一个较大数字是 3。
  对于num1中的数字2，第二个数组中没有下一个更大的数字，因此输出 -1。

示例 2:
输入: nums1 = [2,4], nums2 = [1,2,3,4].
输出: [3,-1]
解释:
    对于num1中的数字2，第二个数组中的下一个较大数字是3。
    对于num1中的数字4，第二个数组中没有下一个更大的数字，因此输出 -1。
注意:

nums1和nums2中所有元素是唯一的。
nums1和nums2 的数组大小都不超过1000。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var nextGreaterElement = function(nums1, nums2) {
  
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
const nextGreaterElement = (nums1, nums2) => {
  const result = [];
  for (let i = 0; i < nums1.length; i++) {
    const index = nums2.findIndex(item2 => item2 === nums1[i]);
    const afterList = nums2.slice(index);
    const afterListIndex = afterList.findIndex(item3 => item3 > nums1[i]);
    if (afterListIndex > -1) {
      result.push(afterList[afterListIndex]);
    } else {
      result.push(afterListIndex);
    }
  }
  return result;
};

// const nums1 = [4, 1, 2];
// const nums2 = [1, 3, 4, 2];
const nums1 = [2, 4];
const nums2 = [1, 2, 3, 4];
console.log(nextGreaterElement(nums1, nums2));
```

`node index.js` 返回：

```js
[3, -1]
```

## 四 LeetCode Submit



```js
Accepted
* 17/17 cases passed (100 ms)
* Your runtime beats 23.6 % of javascript submissions
* Your memory usage beats 5.97 % of javascript submissions (41.2 MB)
```

## 五 解题思路



暴力有时候可以快速解决问题，但是肯定不是最优的解决方式。

**首先**，在这题的破解中，我们遍历 `nums1`，因为 `nums1` 是 `nums2` 的子集，所以在 `nums2` 中 `findIndex` 查找 `nums1` 的元素必定是有的，我们通过 `index` 来记录对应的位置。

**然后**，我们裁剪该 `index` 后 `nums2` 的数组，并在当中查找是否有元素比 `nums1[i]` （当前元素）更大。

**最后**，我们判断是否存在，如果存在则存入该位置对应的值；如果不存在则返回 `-1`（`findIndex` 不存在的时候返回的值）。

这样，我们就完成这个题目啦！（最暴力的方式，排名垫底）

## 六 进一步思考



由于现在 2019-10-29 20:12:13 **jsliang** 还在加班，所以乘测试还在走业务流程，顺带写了这道题，如果小伙伴们有更好的题解或者思路，欢迎留言评论私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

