796 - 旋转字符串（rotate-string）
===

> Create by **jsliang** on **2020-01-05 09:50:38**  
> Recently revised in **2020-01-05 10:06:22**

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
* **题目地址**：https://leetcode-cn.com/problems/rotate-string/
* **题目内容**：

```
给定两个字符串, A 和 B。

A 的旋转操作就是将 A 最左边的字符移动到最右边。
例如, 若 A = 'abcde'，在移动一次之后结果就是'bcdea'。
如果在若干次旋转操作之后，A 能变成 B，那么返回True。

示例 1:
输入: A = 'abcde', B = 'cdeab'
输出: true

示例 2:
输入: A = 'abcde', B = 'abced'
输出: false
注意：

A 和 B 长度不超过 100。=
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} A
 * @param {string} B
 * @return {boolean}
 */
var rotateString = function(A, B) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 旋转字符串
 * @param {string} A
 * @param {string} B
 * @return {boolean}
 */
const rotateString = (A, B) => A.length === B.length && (B + B).includes(A);

console.log(rotateString('abcde', 'cdeab')); // true
console.log(rotateString('abcde', 'abced')); // false
```

`node index.js` 返回：

```js
true
false
```

## 四 LeetCode Submit



```js
Accepted
* 45/45 cases passed (64 ms)
* Your runtime beats 56.73 % of javascript submissions
* Your memory usage beats 21.28 % of javascript submissions (34.2 MB)
```

## 五 解题思路



**智商真的能被提升么？**

> 一行代码

```js
const rotateString = (A, B) => A.length === B.length && (B + B).includes(A);
```

一行破解，enm...毫无挑战。

思路：

1. A 的长度必须和 B 的一样，不管是 A 长还是 B 长，都是否定的结果；
2. 如果 A 旋转得到 B，那么必定会有一件事：两个 B 衔接起来之后，肯定包含了 A。就好比 `'12345'` 和 `'34512'`，当它变换成 `'3451234512'`，你会发现一个规律，两个 B 衔接起来后真的能包含 A。

Submit 提交：

```js
Accepted
* 45/45 cases passed (64 ms)
* Your runtime beats 56.73 % of javascript submissions
* Your memory usage beats 21.28 % of javascript submissions (34.2 MB)
```

当然，如果你有想法，看到 56.73% 和 21.28% 就知道，肯定有大佬又搞了其他操作，将我这破解方法降低了。

欢迎评论留言或者私聊 **jsliang**~

> 内心：好像这期有点水……

> 内心：还真是！

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

