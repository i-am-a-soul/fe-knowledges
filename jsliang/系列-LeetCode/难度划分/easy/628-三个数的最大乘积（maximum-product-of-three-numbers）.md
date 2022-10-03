628 - 三个数的最大乘积（maximum-product-of-three-numbers）
===

> Create by **jsliang** on **2019-11-30 08:38:23**  
> Recently revised in **2019-11-30 09:23:56**

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
* **涉及知识**：数组、数学
* **题目地址**：https://leetcode-cn.com/problems/maximum-product-of-three-numbers/
* **题目内容**：

```
给定一个整型数组，在数组中找出由三个数组成的最大乘积，并输出这个乘积。

示例 1:

输入: [1,2,3]
输出: 6

示例 2:

输入: [1,2,3,4]
输出: 24
注意:

给定的整型数组长度范围是 [3,104]，
数组中所有的元素范围是 [-1000, 1000]。

输入的数组中任意三个数的乘积不会超出 32 位有符号整数的范围。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maximumProduct = function(nums) {
  
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 三个数的最大乘积
 * @param {number[]} nums
 * @return {number}
 */
const maximumProduct = (nums) => {
  nums.sort((a, b) => b - a);
  return Math.max(nums[0] * nums[1] * nums[2], nums[0] * nums[nums.length - 1] * nums[nums.length - 2]);
};

console.log(maximumProduct([1, 2, 3]));
console.log(maximumProduct([1, 2, 3, 4]));
console.log(maximumProduct([-4, -3, -2, -1, 60]));
```

`node index.js` 返回：

```js
6
24
720
```

## 四 LeetCode Submit



```js
Accepted
* 83/83 cases passed (124 ms)
* Your runtime beats 67.23 % of javascript submissions
* Your memory usage beats 48 % of javascript submissions (38.1 MB)
```

## 五 解题思路



**看完题目，思路非常清晰明了**：

1. 排序。从大到小排序或者从小到大排序都可以。假设这里从大到小排序。
2. 计算。两个负数的乘积是正的，所以有两种可能：其一是由前三个数字相乘，得到最大乘积；其二是由前面最大的数相乘于末尾两个数字，得到最大乘积。
3. 举例：`[-4, -3, -2, -1, 60]` 和 `[-3, -4, -1, -2]`。

那么，开始解题：

```js
const maximumProduct = (nums) => {
  nums.sort((a, b) => b - a);
  return Math.max(nums[0] * nums[1] * nums[2], nums[0] * nums[nums.length - 1] * nums[nums.length - 2]);
};
```

Submit 提交：

```js
Accepted
* 83/83 cases passed (124 ms)
* Your runtime beats 67.23 % of javascript submissions
* Your memory usage beats 48 % of javascript submissions (38.1 MB)
```

刚巧及格，成功破题~

## 六 进一步思考



既然这道题变成了找数字，那么我们有没有更优秀的方法，通过一次遍历就可以找到指定的 5 个数字呢？

答案是有的：

```js
const maximumProduct = (nums) => {
  let min1 = Number.MAX_SAFE_INTEGER, // 倒数第一个最小数字
      min2 = Number.MAX_SAFE_INTEGER, // 倒数第二个最小数字
      max1 = Number.MIN_SAFE_INTEGER, // 第一个最大数字
      max2 = Number.MIN_SAFE_INTEGER, // 第二个最大数字
      max3 = Number.MIN_SAFE_INTEGER; // 第三个最大数字
  for (let i = 0; i < nums.length; i++) {
    // 判断前三个最大数字
    if (nums[i] > max1) {
      max3 = max2;
      max2 = max1;
      max1 = nums[i];
    } else if (nums[i] > max2) {
      max3 = max2;
      max2 = nums[i];
    } else if (nums[i] > max3) {
      max3 = nums[i];
    }
    // 判断末两个最小数字
    if (nums[i] < min1) {
      min2 = min1;
      min1 = nums[i];
    } else if (nums[i] < min2) {
      min2 = nums[i];
    }
  }
  return Math.max(max1 * max2 * max3, max1 * min2 * min1);
};
```

小伙伴们小时候经历过 “抢” 弟弟或者妹妹的东西吗？

假设你家里有三个小孩，大娃二娃三娃（`max1`、`max2`、`max3`），每次拿东西，都由大娃优先挑选（因为二娃三娃打不过他啊！）

于是：每次大娃拿到好东西，首先给自己，然后自己的（上一轮最大/最好的东西）丢给二娃，二娃的丢给三娃。

编程思路也是这样：

```js
max3 = max2;
max2 = max1;
max1 = nums[i];
```

最终，我们通过一次 `for` 遍历，让所有的娃都拿到了自己的东西。

Submit 提交结果：

```js
Accepted
* 83/83 cases passed (80 ms)
* Your runtime beats 95.48 % of javascript submissions
* Your memory usage beats 94 % of javascript submissions (37.4 MB)
```

可喜可贺，接近满分~

如果你有更好的思路或者想法，欢迎留言评论或者私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

