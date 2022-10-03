520 - 检测大写字母（detect-capital）
===

> Create by **jsliang** on **2019-11-05 08:28:43**  
> Recently revised in **2019-11-05 09:20:01**

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
* **涉及知识**：字符串
* **题目地址**：https://leetcode-cn.com/problems/detect-capital/
* **题目内容**：

```
给定一个单词，你需要判断单词的大写使用是否正确。

我们定义，在以下情况时，单词的大写用法是正确的：

1. 全部字母都是大写，比如"USA"。
2. 单词中所有字母都不是大写，比如"leetcode"。
3. 如果单词不只含有一个字母，只有首字母大写， 比如 "Google"。

否则，我们定义这个单词没有正确使用大写字母。

示例 1:
输入: "USA"
输出: True

示例 2:
输入: "FlaG"
输出: False
注意: 输入是由大写和小写拉丁字母组成的非空单词。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} word
 * @return {boolean}
 */
var detectCapitalUse = function(word) {
  
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 检测大写字母
 * @param {string} word
 * @return {boolean}
 */
const detectCapitalUse = (word) => {
  // ASCII 对照表
  // a-z：97-122
  // A-Z：65-90
  const wordList = word.split('');
  let index = 0;
  // 全部字母大写 || 首字母大写
  if (wordList[0].charCodeAt() >= 65 && wordList[0].charCodeAt() <= 90) {
    const index1 = wordList.findIndex(item => item.charCodeAt() < 65 || item.charCodeAt() > 90);
    const index2 = wordList.slice(1).findIndex(item => item.charCodeAt() < 97 || item.charCodeAt() > 122);
    index = index1 < index2 ? index1 : index2;
  }
  // 全部字母小写
  if (wordList[0].charCodeAt() >= 97 && wordList[0].charCodeAt() <= 122) {
    index = wordList.findIndex(item => item.charCodeAt() < 97 || item.charCodeAt() > 122);
  }
  return index > -1 ? false : true;
};

// const word = 'USA'; // true
// const word = 'FlaG'; // false
// const word = 'aPple'; // false
// const word = 'apple'; // true
const word = 'Flag'; // true
console.log(detectCapitalUse(word));
```

`node index.js` 返回：

```js
true
```

## 四 LeetCode Submit



```js
Accepted
* 550/550 cases passed (72 ms)
* Your runtime beats 86.43 % of javascript submissions
* Your memory usage beats 56 % of javascript submissions (34 MB)
```

## 五 解题思路



**首先**，拿到题目，检查大写字母判断：

1. 全部字母都是大写，比如"USA"。
2. 单词中所有字母都不是大写，比如"leetcode"。
3. 如果单词不只含有一个字母，只有首字母大写， 比如 "Google"。

即是说，必须完全大写，或者完全小写，再或者首字母大写，这三种情况属于大写字母。

**然后**，**jsliang** 脑海中就浮想起：

* 能不能根据 ASCII 码的值来区分大小写？

已知大小写以及数字的 ASCII 码范围是：

* a-z：97-122
* A-Z：65-90
* 0-9：48-57

写下代码：

```js
/**
 * @name 检测大写字母
 * @param {string} word
 * @return {boolean}
 */
const detectCapitalUse = (word) => {
  // ASCII 对照表
  // a-z：97-122
  // A-Z：65-90
  const wordList = word.split('');
  let index = 0;
  // 全部字母大写 || 首字母大写
  if (wordList[0].charCodeAt() >= 65 && wordList[0].charCodeAt() <= 90) {
    const index1 = wordList.findIndex(item => item.charCodeAt() < 65 || item.charCodeAt() > 90);
    const index2 = wordList.slice(1).findIndex(item => item.charCodeAt() < 97 || item.charCodeAt() > 122);
    index = index1 < index2 ? index1 : index2;
  }
  // 全部字母小写
  if (wordList[0].charCodeAt() >= 97 && wordList[0].charCodeAt() <= 122) {
    index = wordList.findIndex(item => item.charCodeAt() < 97 || item.charCodeAt() > 122);
  }
  return index > -1 ? false : true;
};
```

提交试试：

```js
Accepted
* 550/550 cases passed (72 ms)
* Your runtime beats 86.43 % of javascript submissions
* Your memory usage beats 56 % of javascript submissions (34 MB)
```

Get~ 成功破解本题！

**最后**，讲解下思路：

1. 首字母大写的情况下，如果剩余字母全部大写或者全部小写，都是大写字母
2. 首字母小写的情况下，如果全部字母都是小写，那么就是大写字母
3. 如何判断大小写的，依据 ASCII 即可~

## 六 进一步思考



当然，我们还可以尝试 `toUpperCase()` 和 `toLowerCase()` 的方式来解题：

```js
const detectCapitalUse = (word) => {
  // 全部字母大写
  if (word === word.toUpperCase()) {
    return true;
  }
  // 全部字母小写
  if (word === word.toLowerCase()) {
    return true;
  }
  // 首字母大写
  if (word[0] === word[0].toUpperCase() && word.slice(1) === word.slice(1).toLowerCase()) {
    return true;
  }
  return false;
};
```

Submit 提交：

```js
Accepted
* 550/550 cases passed (72 ms)
* Your runtime beats 86.43 % of javascript submissions
* Your memory usage beats 98.67 % of javascript submissions (33.6 MB)
```

不错不错，帅炸了~

小伙伴们如果有更好的方法，欢迎吐槽，评论留言私聊都可以哈~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

