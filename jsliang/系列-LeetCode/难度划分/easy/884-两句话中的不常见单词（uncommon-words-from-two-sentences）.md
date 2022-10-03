884 - 两句话中的不常见单词（uncommon-words-from-two-sentences）
===

> Create by **jsliang** on **2020-01-14 15:13:54**  
> Recently revised in **2020-01-14 15:45:11**

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
* **题目地址**：
* **题目内容**：https://leetcode-cn.com/problems/uncommon-words-from-two-sentences/

```
给定两个句子 A 和 B。
（句子是一串由空格分隔的单词。每个单词仅由小写字母组成。）

如果一个单词在其中一个句子中只出现一次，
在另一个句子中却没有出现，
那么这个单词就是不常见的。

返回所有不常用单词的列表。

您可以按任何顺序返回列表。

示例 1：

输入：
A = "this apple is sweet", 
B = "this apple is sour"
输出：["sweet","sour"]

示例 2：

输入：
A = "apple apple",
B = "banana"
输出：["banana"]
 
提示：

0 <= A.length <= 200
0 <= B.length <= 200
A 和 B 都只包含空格和小写字母。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} A
 * @param {string} B
 * @return {string[]}
 */
var uncommonFromSentences = function(A, B) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 两句话中的不常见单词
 * @param {string} A
 * @param {string} B
 * @return {string[]}
 */
const uncommonFromSentences = (A, B) => {
  const newArray = (`${A} ${B}`).split(' ');
  const result = [];
  for (let i = 0; i < newArray.length; i++) {
    if (
      newArray.indexOf(newArray[i]) === newArray.lastIndexOf(newArray[i])
      && !result.includes(newArray[i])
    ) {
      result.push(newArray[i]);
    }
  }
  return result;
};

console.log(uncommonFromSentences('this apple is sweet', 'this apple is sour')); // [ 'sweet', 'sour' ]
console.log(uncommonFromSentences('apple apple', 'banana')); // [ 'banana' ]
```

`node index.js` 返回：

```js
[ 'sweet', 'sour' ]
[ 'banana' ]
```

## 四 LeetCode Submit



```js
Accepted
* 53/53 cases passed (60 ms)
* Your runtime beats 90.18 % of javascript submissions
* Your memory usage beats 19.51 % of javascript submissions (34.9 MB)
```

## 五 解题思路



题意导读：

* 如果一个单词在其中一个句子中只出现一次，在另一个句子中却没有出现，那么这个单词就是不常见的。

根据这句话，我是不是可以这样理解：

* 只要这个单词出现的次数小于 2 次，那么这个单词就是不常见的。

那么，我们进行验证：

> 哈希表

```js
const uncommonFromSentences = (A, B) => {
  const newA = A.split(' ');
  const newB = B.split(' ');
  const map = new Map();
  for (let i = 0; i < newA.length; i++) {
    if (map.get(newA[i])) {
      map.set(newA[i], map.get(newA[i]) + 1);
    } else {
      map.set(newA[i], 1);
    }
  }
  for (let i = 0; i < newB.length; i++) {
    if (map.get(newB[i])) {
      map.set(newB[i], map.get(newB[i]) + 1);
    } else {
      map.set(newB[i], 1);
    }
  }
  const result = [];
  for (let [key, value] of map) {
    if (value < 2) {
      result.push(key);
    }
  }
  return result;
};
```

思路：

1. 将 A、B 转换为数组。
2. 设置 `map` 来获取所有哈希表。
3. 遍历 `newA`，取到 A 中的所有单词及其次数。
4. 遍历 `newB`，取都 B 中的所有单词及其次数。

Submit 提交如下：

```js
Accepted
* 53/53 cases passed (80 ms)
* Your runtime beats 13.39 % of javascript submissions
* Your memory usage beats 26.83 % of javascript submissions (34.5 MB)
```

看到这战绩，小伙伴们应该知道我想做啥了：

> 哈希表优化

```js
const uncommonFromSentences = (A, B) => {
  const newArray = (`${A} ${B}`).split(' ');
  const result = [];
  for (let i = 0; i < newArray.length; i++) {
    if (
      newArray.indexOf(newArray[i]) === newArray.lastIndexOf(newArray[i])
      && !result.includes(newArray[i])
    ) {
      result.push(newArray[i]);
    }
  }
  return result;
};
```

主要思路：

1. 将 A 和 B 拼接起来，省得进行二次 `for` 遍历。
2. 设置 `result` 接受结果值。
3. 通过 `for` 遍历新数组，然后判断它的首个索引值和末尾索引值是否相等，并且 `result` 不包含这个元素，就往 `result` 中添加该元素。

Submit 提交如下：

```js
Accepted
* 53/53 cases passed (60 ms)
* Your runtime beats 90.18 % of javascript submissions
* Your memory usage beats 19.51 % of javascript submissions (34.9 MB)
```

这样，我们就完成了这道题的破解及其优化。

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

