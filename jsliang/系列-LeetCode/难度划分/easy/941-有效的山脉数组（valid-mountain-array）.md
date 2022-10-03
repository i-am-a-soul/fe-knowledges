941 - 有效的山脉数组（valid-mountain-array）
===

> Create by **jsliang** on **2020-01-27 16:19:05**  
> Recently revised in **2020-01-27 17:00:48**

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
* **题目地址**：https://leetcode-cn.com/problems/valid-mountain-array/
* **题目内容**：

```
给定一个整数数组 A，如果它是有效的山脉数组就返回 true，否则返回 false。

让我们回顾一下，如果 A 满足下述条件，那么它是一个山脉数组：

A.length >= 3
在 0 < i < A.length - 1 条件下，存在 i 使得：
A[0] < A[1] < ... A[i-1] < A[i]
A[i] > A[i+1] > ... > A[B.length - 1]

示例 1：

输入：[2,1]
输出：false

示例 2：

输入：[3,5,5]
输出：false

示例 3：

输入：[0,3,2,1]
输出：true

提示：

0 <= A.length <= 10000
0 <= A[i] <= 10000 

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/valid-mountain-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} A
 * @return {boolean}
 */
var validMountainArray = function(A) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 有效的山脉数组
 * @param {number[]} A
 * @return {boolean}
 */
const validMountainArray = (A) => {
  // 1. 长度小于 3 判定为 false
  if (A.length < 3) {
    return false;
  }
  // 2. 通过 flag 判断山脉
  let flag = 0;
  for (let i = 0; i < A.length; i++) {
    if (A[i] < A[i + 1] && A[i + 1] > A[i + 2]) {
      flag ++;
    }
    if (A[i] > A[i + 1] && A[i + 1] < A[i + 2]) {
      return false;
    }
    if (A[i] === A[i + 1]) {
      return false;
    }
  }
  return flag === 1;
};

console.log(validMountainArray([0, 3, 2, 1])); // true
console.log(validMountainArray([3, 5, 5])); // false
console.log(validMountainArray([1, 7, 9, 5, 4, 1, 2])); // false
```

`node index.js` 返回：

```js
true
false
false
```

## 四 LeetCode Submit



```js
Accepted
* 51/51 cases passed (128 ms)
* Your runtime beats 6.96 % of javascript submissions
* Your memory usage beats 5.05 % of javascript submissions (39.2 MB)
```

## 五 解题思路



初看很简单，仔细做完头皮发麻：

> 暴力破解

```js
const validMountainArray = (A) => {
  // 1. 长度小于 3 判定为 false
  if (A.length < 3) {
    return false;
  }
  // 2. 通过 flag 判断山脉
  let flag = 0;
  for (let i = 0; i < A.length; i++) {
    if (A[i] < A[i + 1] && A[i + 1] > A[i + 2]) {
      flag ++;
    }
    if (A[i] > A[i + 1] && A[i + 1] < A[i + 2]) {
      return false;
    }
    if (A[i] === A[i + 1]) {
      return false;
    }
  }
  return flag === 1;
};
```

> 以上为细化版，前面还有一版写得较为复杂

题解思路如下：

1. 如果长度小于 3，直接判断为 `false`；
2. 设置 `flag`，判断是否有山脉出现，山脉出现的次数为多少；
3. 通过 `for` 循环山脉，如果是 `i < i + 1 > i + 2`，那么就是山脉，`flag ++`；如果是 `i > i + 1 < i + 2`，那么就是山谷，这时候需要直接返回 `false`，因为这种情况已经不是山脉了；如果是 `i === i + 1`，说明出现了两个一样的数，直接返回 `false` 即可。

这样，通过 `flag` 我们直接掌控全局。

Submit 提交如下：

```js
Accepted
* 51/51 cases passed (76 ms)
* Your runtime beats 50.43 % of javascript submissions
* Your memory usage beats 28.28 % of javascript submissions (37.3 MB)
```

如果小伙伴有更好的思路想法，欢迎评论吐槽或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

