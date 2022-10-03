824 - 山羊拉丁文（goat-latin）
===

> Create by **jsliang** on **2020-01-08 08:43:55**  
> Recently revised in **2020-01-08 09:06:00**

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
* **题目地址**：https://leetcode-cn.com/problems/goat-latin/
* **题目内容**：

```
给定一个由空格分割单词的句子 S。
每个单词只包含大写或小写字母。

我们要将句子转换为 “Goat Latin”
（一种类似于 猪拉丁文 - Pig Latin 的虚构语言）。

山羊拉丁文的规则如下：

如果单词以元音开头（a, e, i, o, u），
在单词后添加"ma"。

例如，单词"apple"变为"applema"。

如果单词以辅音字母开头（即非元音字母），
移除第一个字符并将它放到末尾，之后再添加"ma"。
例如，单词"goat"变为"oatgma"。

根据单词在句子中的索引，
在单词最后添加与索引相同数量的字母'a'，
索引从1开始。

例如，在第一个单词后添加"a"，
在第二个单词后添加"aa"，以此类推。
返回将 S 转换为山羊拉丁文后的句子。

示例 1:

输入: "I speak Goat Latin"
输出: "Imaa peaksmaaa oatGmaaaa atinLmaaaaa"
示例 2:

输入: "The quick brown fox jumped over the lazy dog"
输出: "heTmaa uickqmaaa
rownbmaaaa oxfmaaaaa umpedjmaaaaaa
overmaaaaaaa hetmaaaaaaaa
azylmaaaaaaaaa ogdmaaaaaaaaaa"

说明:

S 中仅包含大小写字母和空格。单词间有且仅有一个空格。
1 <= S.length <= 150。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} S
 * @return {string}
 */
var toGoatLatin = function(S) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 山羊拉丁文
 * @param {string} S
 * @return {string}
 */
const toGoatLatin = (S) => {
  S = S.split(' ');
  for (let i = 0; i < S.length; i++) {
    switch (S[i][0]) {
      case 'a': case 'e': case 'i': case 'o': case 'u':
      case 'A': case 'E': case 'I': case 'O': case 'U':
        S[i] += 'ma' + new Array(i + 2).join('a');
        break;
      default:
        S[i] = S[i].slice(1) + S[i][0] + 'ma' + new Array(i + 2).join('a');
    }
  }
  return S.join(' ');
};

console.log(toGoatLatin('I speak Goat Latin'));
// Imaa peaksmaaa oatGmaaaa atinLmaaaaa
```

`node index.js` 返回：

```js
Imaa peaksmaaa oatGmaaaa atinLmaaaaa
```

## 四 LeetCode Submit



```js
Accepted
* 99/99 cases passed (68 ms)
* Your runtime beats 61.45 % of javascript submissions
* Your memory usage beats 17.39 % of javascript submissions (35.2 MB)
```

## 五 解题思路



之前说过，越长的题目，反而越发清晰怎么计算：

```js
const toGoatLatin = (S) => {
  S = S.split(' ');
  for (let i = 0; i < S.length; i++) {
    switch (S[i][0]) {
      case 'a': case 'e': case 'i': case 'o': case 'u':
      case 'A': case 'E': case 'I': case 'O': case 'U':
        S[i] += 'ma' + new Array(i + 2).join('a');
        break;
      default:
        S[i] = S[i].slice(1) + S[i][0] + 'ma' + new Array(i + 2).join('a');
    }
  }
  return S.join(' ');
};
```

在这题中，我们牢记 3 个准则：

1. 开头字母为元音字母 `a/e/i/o/u` 或者 `A/E/I/O/U` 的单词后面添加 `ma`；
2. 除元音字母外开头的单词，先将开头字母移动到后面，再添加 `ma`；
3. 从 `index = 0` 的字母添加一个 `a` 开始，往后不停增长 `a` 的长度到 `S.length`；

这样，我们就有了这个题解。

Submit 提交：

```js
Accepted
* 99/99 cases passed (68 ms)
* Your runtime beats 61.45 % of javascript submissions
* Your memory usage beats 17.39 % of javascript submissions (35.2 MB)
```

enm...这么说这样子还是挺无聊的，也没有在【题解区】和【评论区】找到比较有意思的题解~

如果你有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

