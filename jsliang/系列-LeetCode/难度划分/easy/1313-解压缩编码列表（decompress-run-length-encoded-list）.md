1313 - 解压缩编码列表（decompress-run-length-encoded-list）
===

> Create by **jsliang** on **2020-02-01 20:22:55**  
> Recently revised in **2020-02-01 20:35:13**

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
* **题目地址**：https://leetcode-cn.com/problems/decompress-run-length-encoded-list/
* **题目内容**：

```
给你一个以行程长度编码压缩的整数列表 nums 。

考虑每对相邻的两个元素
[a, b] = [nums[2*i], nums[2*i+1]]
（其中 i >= 0 ），
每一对都表示解压后有 a 个值为 b 的元素。

请你返回解压后的列表。

示例：

输入：nums = [1,2,3,4]
输出：[2,4,4,4]
解释：
第一对 [1,2] 代表着 2 的出现频次为 1，所以生成数组 [2]。
第二对 [3,4] 代表着 4 的出现频次为 3，所以生成数组 [4,4,4]。
最后将它们串联到一起 [2] + [4,4,4,4] = [2,4,4,4]。

提示：

2 <= nums.length <= 100
nums.length % 2 == 0
1 <= nums[i] <= 100

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/decompress-run-length-encoded-list
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var decompressRLElist = function(nums) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 解压缩编码列表
 * @param {number[]} nums
 * @return {number[]}
 */
const decompressRLElist = (nums) => {
  const result = [];
  for (let i = 1; i < nums.length; i++) {
    if (i % 2 === 1) {
      result.push(...Array.from(Array(nums[i - 1]), () => nums[i]));
    }
  }
  return result;
};

console.log(decompressRLElist([1, 2, 3, 4])); // [2, 4, 4, 4]
```

`node index.js` 返回：

```js
[2, 4, 4, 4]
```

## 四 LeetCode Submit



```js
Accepted
* 52/52 cases passed (148 ms)
* Your runtime beats 5.08 % of javascript submissions
* Your memory usage beats 100 % of javascript submissions (37.1 MB)
```

## 五 解题思路



首先，我们分析下题目：

* 第 奇数位 为需要生成的次数
* 第 偶数位 为对应需要生产的数字

那么就有：

> 暴力破解

```js
const decompressRLElist = (nums) => {
  const result = [];
  for (let i = 1; i < nums.length; i++) {
    if (i % 2 === 1) {
      result.push(...Array.from(Array(nums[i - 1]), () => nums[i]));
    }
  }
  return result;
};
```

我们只判断奇数位，然后通过 `Array.from(i+1, () => i)` 的形式，生成 `n` 个 `nums[i]`。

Submit 提交：

```js
Accepted
* 52/52 cases passed (148 ms)
* Your runtime beats 5.08 % of javascript submissions
* Your memory usage beats 100 % of javascript submissions (37.1 MB)
```

再次收获一次空间 100% 打败的记录。

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

