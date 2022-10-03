1295 - 统计位数为偶数的数字（find-numbers-with-even-number-of-digits）
===

> Create by **jsliang** on **2020-02-01 18:55:24**  
> Recently revised in **2020-02-01 19:02:38**

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
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/find-numbers-with-even-number-of-digits/
* **题目内容**：

```
给你一个整数数组 nums，
请你返回其中位数为 偶数 的数字的个数。

示例 1：

输入：nums = [12,345,2,6,7896]
输出：2
解释：
12 是 2 位数字（位数为偶数） 
345 是 3 位数字（位数为奇数）  
2 是 1 位数字（位数为奇数） 
6 是 1 位数字 位数为奇数） 
7896 是 4 位数字（位数为偶数）  
因此只有 12 和 7896 是位数为偶数的数字

示例 2：

输入：nums = [555,901,482,1771]
输出：1 
解释： 
只有 1771 是位数为偶数的数字。

提示：

1 <= nums.length <= 500
1 <= nums[i] <= 10^5

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-numbers-with-even-number-of-digits
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findNumbers = function(nums) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 统计位数为偶数的数字
 * @param {number[]} nums
 * @return {number}
 */
const findNumbers = (nums) => {
  let time = 0;
  for (let i = 0; i < nums.length; i++) {
    if (String(nums[i]).length % 2 === 0) {
      time++;
    }
  }
  return time;
};

console.log(findNumbers([12, 345, 2, 6, 7896])); // 2
```

`node index.js` 返回：

```js
2
```

## 四 LeetCode Submit



```js
Accepted
* 102/102 cases passed (68 ms)
* Your runtime beats 67.89 % of javascript submissions
* Your memory usage beats 87.97 % of javascript submissions (35.2 MB)
```

## 五 解题思路



如果要秀的话，那就是一行求解：

> 一行求解

```js
const findNumbers = (nums) => nums.reduce((prev, next) => prev + (String(next).length % 2 === 0 ? 1 : 0), 0);
```

Submit 提交：

```js
Accepted
* 102/102 cases passed (76 ms)
* Your runtime beats 22.77 % of javascript submissions
* Your memory usage beats 85.34 % of javascript submissions (35.2 MB)
```

如果小伙伴想看清楚的话，那就转成多行：

> 暴力破解

```js
const findNumbers = (nums) => {
  let time = 0;
  for (let i = 0; i < nums.length; i++) {
    if (String(nums[i]).length % 2 === 0) {
      time++;
    }
  }
  return time;
};
```

Submit 提交：

```js
Accepted
* 102/102 cases passed (68 ms)
* Your runtime beats 67.89 % of javascript submissions
* Your memory usage beats 87.97 % of javascript submissions (35.2 MB)
```

当然，也许还有其他法子，但是我觉得杀鸡焉用牛刀，两种就够用了~

如果小伙伴还有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

