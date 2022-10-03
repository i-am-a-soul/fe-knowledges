541 - 反转字符串II（reverse-string-ii）
===

> Create by **jsliang** on **2019-11-10 13:16:42**  
> Recently revised in **2019-11-10 13:53:02**

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
* **题目地址**：https://leetcode-cn.com/problems/reverse-string-ii/
* **题目内容**：

```
给定一个字符串和一个整数 

你需要对从字符串开头算起的每个 2k 个字符的前k个字符进行反转

如果剩余少于 k 个字符，则将剩余的所有全部反转。

如果有小于 2k 但大于或等于 k 个字符，则反转前 k 个字符，并将剩余的字符保持原样。

示例:

输入: s = "abcdefg", k = 2
输出: "bacdfeg"

要求:
该字符串只包含小写的英文字母。
给定字符串的长度和 k 在[1, 10000]范围内。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var reverseStr = function(s, k) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 反转字符串II
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
const reverseStr = (s, k) => {
  s = s.split('');
  const result = [];
  while (s.length) {
    result.push(s.splice(0, 2 * k));
  }
  for (let i = 0; i < result.length; i++) {
    if (result[i].length < k) {
      result[i].reverse();
    }
    if (result[i].length >= k && result[i].length <= 2 * k) {
      const leftHarf = result[i].slice(0, k);
      const rightHarf = result[i].slice(k);
      result[i] = [...leftHarf.reverse(), ...rightHarf];
    }
  }
  return result.map(item => item.join('')).join('');
};

console.log(reverseStr('abcdefg', 2));
```

`node index.js` 返回：

```js
bacdfeg
```

## 四 LeetCode Submit



```js
Accepted
* 60/60 cases passed (80 ms)
* Your runtime beats 61.72 % of javascript submissions
* Your memory usage beats 45.45 % of javascript submissions (37.6 MB)
```

## 五 解题思路



首先看题，又是长篇大论然后就给了一个示例，想想要先试探几次就感觉不嗨皮啊！

```js
/**
 * @name 反转字符串II
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
const reverseStr = (s, k) => {
  s = s.split('');
  const result = [];
  while (s.length) {
    result.push(s.splice(0, 2 * k));
  }
  for (let i = 0; i < result.length; i++) {
    if (result[i].length < k) {
      result[i].reverse();
    }
    if (result[i].length >= k && result[i].length <= 2 * k) {
      const leftHarf = result[i].slice(0, k);
      const rightHarf = result[i].slice(k);
      result[i] = [...leftHarf.reverse(), ...rightHarf];
    }
  }
  return result.map(item => item.join('')).join('');
};
```

Submit 试试：

```js
Accepted
* 60/60 cases passed (80 ms)
* Your runtime beats 61.72 % of javascript submissions
* Your memory usage beats 45.45 % of javascript submissions (37.6 MB)
```

真失败！！！

这么混乱的垃圾提交都通过了，哭~

讲讲思路：

1. 已知字符串： `abcdefg`。
2. 通过 `while` 循环，尝试按照 2k 长度进行分割：`[ [ 'a', 'b', 'c', 'd' ], [ 'e', 'f', 'g' ] ]`。
3. 通过 `for` 循环，将数组按照规矩进行翻转：
   1. 如果长度小于 k，则所有内容翻转。
   2. 如果长度大于或者等于 k，且小于或者等于 2k，那么将其拆分成两半，左半边翻转，右半边原样。
4. 最后将每个二维数组转换成字符串，再将一位数组转换成字符串。

很好，成功将一些小伙伴整懵逼~

如果你有更好的法子或者更清晰的思路，欢迎评论吐槽或者直接私聊捶我~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

