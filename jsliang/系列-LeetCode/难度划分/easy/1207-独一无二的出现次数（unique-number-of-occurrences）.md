1207 - 独一无二的出现次数（unique-number-of-occurrences）
===

> Create by **jsliang** on **2020-01-31 21:41:54**  
> Recently revised in **2020-01-31 22:00:31**

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
* **涉及知识**：哈希表
* **题目地址**：https://leetcode-cn.com/problems/unique-number-of-occurrences/
* **题目内容**：

```
给你一个整数数组 arr，
请你帮忙统计数组中每个数的出现次数。

如果每个数的出现次数都是独一无二的，
就返回 true；否则返回 false。

示例 1：

输入：arr = [1,2,2,1,1,3]
输出：true
解释：
在该数组中，
1 出现了 3 次，
2 出现了 2 次，
3 只出现了 1 次。
没有两个数的出现次数相同。

示例 2：

输入：arr = [1,2]
输出：false

示例 3：

输入：arr = [-3,0,1,-3,1,1,1,-3,10,0]
输出：true

提示：

1 <= arr.length <= 1000
-1000 <= arr[i] <= 1000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/unique-number-of-occurrences
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} arr
 * @return {boolean}
 */
var uniqueOccurrences = function(arr) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 独一无二的出现次数
 * @param {number[]} arr
 * @return {boolean}
 */
const uniqueOccurrences = (arr) => {
  const listMap = new Map();
  for (let i = 0; i < arr.length; i++) {
    if (listMap.has(arr[i])) {
      listMap.set(arr[i], listMap.get(arr[i]) + 1);
    } else {
      listMap.set(arr[i], 1);
    }
  }
  const timeMap = new Map();
  for (const [key, value] of listMap) {
    if (timeMap.has(value)) {
      return false;
    } else {
      timeMap.set(value, 1);
    }
  }
  return true;
};

console.log(uniqueOccurrences([1, 2, 2, 1, 1, 3])); // true
console.log(uniqueOccurrences([1, 2])); // false
console.log(uniqueOccurrences([-3, 0, 1, -3, 1, 1, 1, -3, 10, 0])); // true
```

`node index.js` 返回：

```js
true
false
true
```

## 四 LeetCode Submit



```js
Accepted
* 63/63 cases passed (60 ms)
* Your runtime beats 91.03 % of javascript submissions
* Your memory usage beats 97 % of javascript submissions (33.7 MB)
```

## 五 解题思路



对于这道题，**jsliang** 的思路是设置两个哈希表：

1. 哈希表 `listMap` 统计列表数字出现的次数；
2. 哈希表 `timeMap` 记录都有哪些数字。

OK，咱实现试试：

> 哈希表

```js
const uniqueOccurrences = (arr) => {
  // 1. listMap 获取每个数字出现的次数
  const listMap = new Map();
  for (let i = 0; i < arr.length; i++) {
    if (listMap.has(arr[i])) {
      listMap.set(arr[i], listMap.get(arr[i]) + 1);
    } else {
      listMap.set(arr[i], 1);
    }
  }
  // 2. timeMap 判断数字是否重复
  const timeMap = new Map();
  for (const [key, value] of listMap) {
    if (timeMap.has(value)) {
      return false;
    } else {
      timeMap.set(value, 1);
    }
  }
  return true;
};
```

Submit 提交：

```js
Accepted
* 63/63 cases passed (60 ms)
* Your runtime beats 91.03 % of javascript submissions
* Your memory usage beats 97 % of javascript submissions (33.7 MB)
```

想来也是简简单单~

## 六 进一步思考



在题解区看到使用 `Set` 的大佬，感觉也是极好的：

```js
const uniqueOccurrences = (arr) => {
  const keyArr = [];
  const countArr = [];
  keyArr = Array.from(new Set(arr));
  for (let i = 0; i < keyArr.length; i++) {
    countArr.push(0);
  }
  for (let i = 0; i < arr.length; i++) {
    countArr[keyArr.indexOf(arr[i])]++;
  }
  if (Array.from(new Set(countArr)).length == countArr.length) {
    return true;
  } else {
    return false;
  }
};
```

Submit 提交：

```js
Accepted
* 63/63 cases passed (52 ms)
* Your runtime beats 98.94 % of javascript submissions
* Your memory usage beats 90.39 % of javascript submissions (33.9 MB)
```

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

