748 - 最短完整词（shortest-completing-word）
===

> Create by **jsliang** on **2020-1-1 17:45:07**  
> Recently revised in **2020-1-1 18:49:38**

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
* **涉及知识**：哈希表
* **题目地址**：https://leetcode-cn.com/problems/shortest-completing-word/
* **题目内容**：

```
如果单词列表（words）中，
一个单词包含牌照（licensePlate）中所有的字母，
那么我们称之为完整词。
在所有完整词中，最短的单词我们称之为最短完整词。

单词在匹配牌照中的字母时不区分大小写，
比如牌照中的 "P" 依然可以匹配单词中的 "p" 字母。

我们保证一定存在一个最短完整词。
当有多个单词都符合最短完整词的匹配条件时，
取单词列表中最靠前的一个。

牌照中可能包含多个相同的字符，
比如说：对于牌照 "PP"，单词 "pair" 无法匹配，
但是 "supper" 可以匹配。

示例 1：

输入：
licensePlate = "1s3 PSt",
words = ["step", "steps", "stripe", "stepple"]
输出："steps"
说明：最短完整词应该包括 "s"、"p"、"s" 以及 "t"。
对于 "step" 它只包含一个 "s" 所以它不符合条件。
同时在匹配过程中我们忽略牌照中的大小写。
 
示例 2：

输入：
licensePlate = "1s3 456", 
words = ["looks", "pest", "stew", "show"]
输出："pest"
说明：存在 3 个包含字母 "s" 且有着最短长度的完整词，
但我们返回最先出现的完整词。

注意:

牌照（licensePlate）的长度在区域[1, 7]中。
牌照（licensePlate）将会包含数字、空格、
或者字母（大写和小写）。
单词列表（words）长度在区间 [10, 1000] 中。
每一个单词 words[i] 都是小写，并且长度在区间 [1, 15] 中。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} licensePlate
 * @param {string[]} words
 * @return {string}
 */
var shortestCompletingWord = function(licensePlate, words) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 最短完整词
 * @param {string} licensePlate
 * @param {string[]} words
 * @return {string}
 */
const shortestCompletingWord = (licensePlate, words) => {
  licensePlate = licensePlate.toLowerCase().split('').filter(item => item.charCodeAt() >= 97 && item.charCodeAt() <= 122);
  const map = new Map();
  for (let i = 0; i < licensePlate.length; i++) {
    if (map.has(licensePlate[i])) {
      map.set(licensePlate[i], map.get(licensePlate[i]) + 1);
    } else {
      map.set(licensePlate[i], 1);
    }
  }
  let flag;
  const result = [];
  let minLength = Number.MAX_SAFE_INTEGER;
  for (let i = 0; i < words.length; i++) {
    flag = false;
    for (let [key, value] of map) {
      const filter = words[i].split('').filter(item => item === key);
      if (filter.length < value) {
        flag = true;
        continue;
      }
    }
    if (!flag) {
      result.push(words[i]);
      if (words[i].length < minLength) {
        minLength = words[i].length;
      }
    };
  }
  return result.find(item => item.length === minLength);
};

// console.log(shortestCompletingWord('1s3 PSt', ['step', 'steps', 'stripe', 'stepple'])); // steps
// console.log(shortestCompletingWord('1s3 456', ['looks', 'pest', 'stew', 'show'])); // pest
console.log(shortestCompletingWord('GrC8950', ['measure','other','every','base','according','level','meeting','none','marriage','rest'])); // according
```

`node index.js` 返回：

```js
according
```

## 四 LeetCode Submit



```js
Accepted
* 102/102 cases passed (88 ms)
* Your runtime beats 66.67 % of javascript submissions
* Your memory usage beats 5.55 % of javascript submissions (42.7 MB)
```

## 五 解题思路



糟糕的体验，写完整道题懵逼了：

```js
Accepted
* 102/102 cases passed (88 ms)
* Your runtime beats 66.67 % of javascript submissions
* Your memory usage beats 5.55 % of javascript submissions (42.7 MB)
```

内心真是 5.55……

我给的答案真的不是一般的复杂，贴出来我也不知道从哪讲起，你品，你细细地品：

```js
const shortestCompletingWord = (licensePlate, words) => {
  licensePlate = licensePlate.toLowerCase().split('').filter(item => item.charCodeAt() >= 97 && item.charCodeAt() <= 122);
  const map = new Map();
  for (let i = 0; i < licensePlate.length; i++) {
    if (map.has(licensePlate[i])) {
      map.set(licensePlate[i], map.get(licensePlate[i]) + 1);
    } else {
      map.set(licensePlate[i], 1);
    }
  }
  let flag;
  const result = [];
  let minLength = Number.MAX_SAFE_INTEGER;
  for (let i = 0; i < words.length; i++) {
    flag = false;
    for (let [key, value] of map) {
      const filter = words[i].split('').filter(item => item === key);
      if (filter.length < value) {
        flag = true;
        continue;
      }
    }
    if (!flag) {
      result.push(words[i]);
      if (words[i].length < minLength) {
        minLength = words[i].length;
      }
    };
  }
  return result.find(item => item.length === minLength);
};
```

尽在无言对眼中……

如果你有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

