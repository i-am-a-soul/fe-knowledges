665 - 非递减数列（non-decreasing-array）
===

> Create by **jsliang** on **2019-12-8 10:21:54**  
> Recently revised in **2019-12-8 12:02:14**

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
* **题目地址**：https://leetcode-cn.com/problems/non-decreasing-array/
* **题目内容**：

```
给定一个长度为 n 的整数数组，
你的任务是判断在最多改变 1 个元素的情况下，
该数组能否变成一个非递减数列。

我们是这样定义一个非递减数列的：
对于数组中所有的 i (1 <= i < n)，
满足 array[i] <= array[i + 1]。

示例 1:
输入: [4,2,3]
输出: True
解释: 
你可以通过把第一个 4 变成 1 来使得它成为一个非递减数列。

示例 2:
输入: [4,2,1]
输出: False
解释: 你不能在只改变一个元素的情况下将其变为非递减数列。

说明:  n 的范围为 [1, 10,000]。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var checkPossibility = function(nums) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 非递减数列
 * @param {number[]} nums
 * @return {boolean}
 */
const checkPossibility = (nums) => {
  let count = 0;
  for (let i = 0; i < nums.length; i++) {
    const prev = nums[i - 1];
    const now = nums[i];
    const next = nums[i + 1];
    const nextNext = nums[i + 2];
    if (now > next) {
      count ++;
      if (count > 1) {
        return false;
      }
      if (i > 0 && prev > next && i + 2 < nums.length && now > nextNext) {
        return false;
      }
    }
  }
  return true;
};

console.log(checkPossibility([1, 5, 4, 6, 7, 10, 10, 8, 9]));
```

`node index.js` 返回：

```js
false
```

## 四 LeetCode Submit



```js
执行结果：通过

执行用时：64 ms，在所有 JavaScript 提交中击败了 98.56% 的用户

内存消耗：37.1 MB，在所有 JavaScript 提交中击败了 27.59% 的用户
```

## 五 解题思路



**一顿操作猛如虎，只怕最终渣成土**。

> 失败题解，仅供嘲讽

```js
const checkPossibility = (nums) => {
  let count = 0;
  for (let i = 0; i < nums.length; i++) {
    // [4, 2, 1] - 递减无解
    if (nums[i] > nums[i + 1] && nums[i + 1] > nums[i + 2]) {
      return false;
    }
    // [2, 3, 3, 2, 4] - 有解
    // [4, 2, 3] - 有解
    // [-1, 4, 2, 3] - 有解
    // [3, 4, 2, 3] - 无解
    // [1, 3, 2, 5, 4] - 无解
    // [1, 5, 4, 6, 7, 10, 10, 8, 9] - 无解
    // [3, 2, 3, 2, 4] - 无解
    if (nums[i] > nums[i - 1] && nums[i] > nums[i + 1] && nums[i + 1] > nums[i - 1]) {
      nums[i] = nums[i - 1];
      count ++;
    }
    if (nums[i] >= nums[i - 1] && nums[i] > nums[i + 1] && nums[i + 1] < nums[i - 1]) {
      nums[i] = nums[i - 1];
      count ++;
    }
    if (nums[i] < nums[i - 1] && nums[i] < nums[i - 1] && nums[i + 1] >= nums[i - 1]) {
      nums[i] = nums[i - 1];
      count ++;
    }
    if (count > 1) {
      return false;
    }
  }
  return true;
};
```

是的，你没看错，那些注释就是我曾经的失败的例子，然后经过 long long 的解题，还是失败了……

难受啊！

仔细思考了一下，3 个数始终有误判，咱还不能判断 4 个数吗？恶由胆边生：

```js
const checkPossibility = (nums) => {
  let count = 0;
  for (let i = 0; i < nums.length; i++) {
    const prev = nums[i - 1];
    const now = nums[i];
    const next = nums[i + 1];
    const nextNext = nums[i + 2];
    if (now > next) {
      count ++;
      if (count > 1) {
        return false;
      }
      if (i > 0 && i + 2 < nums.length && prev > next && now > nextNext) {
        return false;
      }
    }
  }
  return true;
};
```

思路如下：

1. 通过 `count` 计数。
2. 遍历 `nums`。
3. 通过 `prev`、`now`、`next`、`nextNext` 记录一组数字。
4. 判断当前值 `now` 是否比下一个值 `next` 大，是的话就将计数器 `count ++`，计数器大于一次就返回 `false`。
5. 判断当前数组是否足够 `4` 长度，够的话就将前一个和下一个比较 `prev > next`，当前一个和下下一个比较 `now > nextNext`。如果这两个比较都是 `true` 的话，说明这个数列没救了。举例：`3, 4, 2, 3`。

Submit 提交；

```js
执行结果：通过

执行用时：64 ms，在所有 JavaScript 提交中击败了 98.56% 的用户

内存消耗：37.1 MB，在所有 JavaScript 提交中击败了 27.59% 的用户
```

OK，因为这次 VS Code 的插件还坏了，所以每次搞起来不太顺手，题目做得也就，好歹最终搞定了。

如果小伙伴们有更好的思路或者想法，欢迎评论留言或者私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

