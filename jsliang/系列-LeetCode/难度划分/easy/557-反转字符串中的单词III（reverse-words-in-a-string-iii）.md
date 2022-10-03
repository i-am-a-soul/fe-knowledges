557 - 反转字符串中的单词III（reverse-words-in-a-string-iii）
===

> Create by **jsliang** on **2019-11-13 08:24:02**  
> Recently revised in **2019-11-13 08:53:29**

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
* **题目地址**：https://leetcode-cn.com/problems/reverse-words-in-a-string-iii/
* **题目内容**：

```
给定一个字符串，你需要反转字符串中每个单词的字符顺序。

同时仍保留空格和单词的初始顺序。

示例 1:

输入: "Let's take LeetCode contest"
输出: "s'teL ekat edoCteeL tsetnoc" 

注意：

在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} s
 * @return {string}
 */
var reverseWords = function(s) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 反转字符串中的单词III
 * @param {string} s
 * @return {string}
 */
const reverseWords = (s) => {
  s = s.split(' ');
  for (let i = 0; i < s.length; i++) {
    s[i] = s[i].split('').reverse().join('');
  }
  return s.join(' ');
};

console.log(reverseWords(`Let's take LeetCode contest`));
// s'teL ekat edoCteeL tsetnoc
```

`node index.js` 返回：

```
s'teL ekat edoCteeL tsetnoc
```

## 四 LeetCode Submit



```js
Accepted
* 30/30 cases passed (92 ms)
* Your runtime beats 83.51 % of javascript submissions
* Your memory usage beats 60.67 % of javascript submissions (42.3 MB)
```

## 五 解题思路



这道题简单我先来~

```js
const reverseWords = (s) => {
  s = s.split(' ');
  for (let i = 0; i < s.length; i++) {
    s[i] = s[i].split('').reverse().join('');
  }
  return s.join(' ');
};
```

Submit 提交：

```js
Accepted
* 30/30 cases passed (92 ms)
* Your runtime beats 83.51 % of javascript submissions
* Your memory usage beats 60.67 % of javascript submissions (42.3 MB)
```

搞定完事，说说思路：

1. 通过空格分割这个字符串为数组。
2. 遍历这个数组，将数组中的每个元素打成数组，反转后再打成字符串。
3. 最后将数组以空格分开的形式转换成字符串。

## 六 进一步思考



这道题肯定有其他解法，但是我不太想去了解，毕竟我觉得这道题没有更深层次的内涵可以挖掘。

1. 你可以使用原生方式，抛弃 JavaScript API 编写
2. 你可以换其他 JavaScript API 进行编写，但是感觉差不到哪

当然，如果你有更多精巧的方式，欢迎评论留言或者私聊我~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

