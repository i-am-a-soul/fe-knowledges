806 - 写字符串需要的行数（number-of-lines-to-write-string）
===

> Create by **jsliang** on **2020-01-05 16:53:55**  
> Recently revised in **2020-01-05 17:15:39**

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
* **涉及知识**：字符串
* **题目地址**：
* **题目内容**：

```
我们要把给定的字符串 S 从左到右写到每一行上，
每一行的最大宽度为 100 个单位，
如果我们在写某个字母的时候会使这行超过了 100 个单位，
那么我们应该把这个字母写到下一行。

我们给定了一个数组 widths，
这个数组 widths[0] 代表 'a' 需要的单位，
widths[1] 代表 'b' 需要的单位，...，
 widths[25] 代表 'z' 需要的单位。

现在回答两个问题：
至少多少行能放下 S，
以及最后一行使用的宽度是多少个单位？
将你的答案作为长度为 2 的整数列表返回。

示例 1:
输入: 
widths = [10,10,10,10,10,10,
10,10,10,10,10,10,10,10,10,10,
10,10,10,10,10,10,10,10,10,10]
S = "abcdefghijklmnopqrstuvwxyz"
输出: [3, 60]
解释: 
所有的字符拥有相同的占用单位 10。所以书写所有的 26 个字母，
我们需要 2 个整行和占用 60 个单位的一行。

示例 2:
输入: 
widths = [4,10,10,10,10,10,10,
10,10,10,10,10,10,10,10,10,10,
10,10,10,10,10,10,10,10,10]
S = "bbbcccdddaaa"
输出: [2, 4]
解释: 
除去字母 'a' 所有的字符都是相同的单位 10，
并且字符串 "bbbcccdddaa" 将会覆盖 9 * 10 + 2 * 4 = 98 个单位.
最后一个字母 'a' 将会被写到第二行，因为第一行只剩下2个单位了。
所以，这个答案是2行，第二行有4个单位宽度。
 
注:

字符串 S 的长度在 [1, 1000] 的范围。
S 只包含小写字母。
widths 是长度为 26的数组。
widths[i] 值的范围在 [2, 10]。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} widths
 * @param {string} S
 * @return {number[]}
 */
var numberOfLines = function(widths, S) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 写字符串需要的行数
 * @param {number[]} widths
 * @param {string} S
 * @return {number[]}
 */
const numberOfLines = (widths, S) => {
  const row = [];
  let rowMark = 0;
  for (let i = 0; i < S.length; i++) {
    const tempMark = widths[S[i].charCodeAt() - 97];
    if (rowMark + tempMark > 100) {
      row.push(rowMark);
      rowMark = tempMark;
    } else {
      rowMark += tempMark;
    }
  }
  row.push(rowMark);
  return [row.length, row[row.length - 1]];
};

console.log(
  numberOfLines(
    [10, 10, 10, 10, 10,
     10, 10, 10, 10, 10,
     10, 10, 10, 10, 10,
     10, 10, 10, 10, 10,
     10, 10, 10, 10, 10, 10
    ],
    'abcdefghijklmnopqrstuvwxyz',
  ),
);
```

`node index.js` 返回：

```js
[3, 60]
```

## 四 LeetCode Submit



```js
Accepted
* 26/26 cases passed (60 ms)
* Your runtime beats 93.48 % of javascript submissions
* Your memory usage beats 46.15 % of javascript submissions (34.9 MB)
```

## 五 解题思路



**谨且记住：如果题目描述地很复杂，说不定它很简单；如果题目描述的很简单，说不定它很难。**

给点精神，仔细读题：

1. 有一个 26 个长度的数组 `widths`，代表这 26 个字母所占的位置。如果你想更清晰点的话，你可以看成一个人，写的 26 个字母可能会占的位置大小（有些人写字大，有的人写字小）。
2. 有一个 [1, 1000] 长度的字符串 `S`，我们要做的就是将它占用的行数，以及它最后一行的数字 `show` 出来。
3. 值得注意的是：如果当前行到了 90，但是下一个字母占用的位置是 11，那么应该换行重新输入。

```js
const numberOfLines = (widths, S) => {
  const row = [];
  let rowMark = 0;
  for (let i = 0; i < S.length; i++) {
    const tempMark = widths[S[i].charCodeAt() - 97];
    if (rowMark + tempMark > 100) {
      row.push(rowMark);
      rowMark = tempMark;
    } else {
      rowMark += tempMark;
    }
  }
  row.push(rowMark);
  return [row.length, row[row.length - 1]];
};
```

看到这里，我们假设一个条件，应该是怎样的：

```js
console.log(
  numberOfLines(
    [10, 10, 10, 10, 10,
     10, 10, 10, 10, 10,
     10, 10, 10, 10, 10,
     10, 10, 10, 10, 10,
     10, 10, 10, 10, 10, 10
    ],
    'abcdefghijklmnopqrstuvwxyz',
  ),
);
row = [100, 100, 60]
```

仔细看：

1. `S` 是从 `a-z` 的 26 个字母；
2. 它们对应的 `widths` 占用的位置都是 10，意味着每行恰好填充上 100；
3. 所以 `row` 最后应该是 `[100, 100, 60]`。

Submit 提交如下：

```js
Accepted
* 26/26 cases passed (60 ms)
* Your runtime beats 93.48 % of javascript submissions
* Your memory usage beats 46.15 % of javascript submissions (34.9 MB)
```

如果你没看懂，或者你有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

