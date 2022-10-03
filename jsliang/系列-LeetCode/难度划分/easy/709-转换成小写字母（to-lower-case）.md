709 - 转换成小写字母（to-lower-case）
===

> Create by **jsliang** on **2019-12-22 12:05:53**  
> Recently revised in **2019-12-22 12:38:17**

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
* **题目地址**：https://leetcode-cn.com/problems/to-lower-case/
* **题目内容**：

```
实现函数 ToLowerCase()，
该函数接收一个字符串参数 str，
并将该字符串中的大写字母转换成小写字母，
之后返回新的字符串。

示例 1：

输入: "Hello"
输出: "hello"
示例 2：

输入: "here"
输出: "here"
示例 3：

输入: "LOVELY"
输出: "lovely"
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} str
 * @return {string}
 */
var toLowerCase = function(str) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 转换成小写字母
 * @param {string} str
 * @return {string}
 */
const toLowerCase = (str) => {
  let result = '';
  for (let i = 0; i < str.length; i++) {
    if (str[i] > 'A' && str[i] < 'Z') {
      result += String.fromCharCode(str[i].charCodeAt() + 32);
    } else {
      result += str[i];
    }
  }
  return result;
};

console.log(toLowerCase('Hello'));
```

`node index.js` 返回：

```js
'hello'
```

## 四 LeetCode Submit



```js
Accepted
* 8/8 cases passed (68 ms)
* Your runtime beats 32.54 % of javascript submissions
* Your memory usage beats 5.16 % of javascript submissions (34.4 MB)
```

## 五 解题思路



**程序员都是懒人，过一会回来再问回复还是这个！**

> 直接使用 API

```js
const toLowerCase = (str) => {
  return str.toLowerCase();
};
```

Submit 提交：

```js
Accepted
* 8/8 cases passed (60 ms)
* Your runtime beats 78.81 % of javascript submissions
* Your memory usage beats 5.16 % of javascript submissions (34.4 MB)
```

enm...原生的也只有这么低，看来有大佬写了个更好的啊~

说到这里，小伙伴们知道 `toLowerCase()` 和 `toLocaleLowerCase()` 的区别是啥么？

* `toLowerCase()`：借鉴于 java.lang.String 的同名方法，转换成小写。
* `toLocaleLowerCase()`：针对特定地区的实现，如土耳其语言等会应用特殊的规则，这时候就需要这个方法来保证实现正确。

> 如果你的代码可能会在多种语言环境中使用的话，还是 `toLocaleLowerCase()` 吧~

然后咱们用哈希表实现吧：

> 哈希表

```js
/**
 * @name 哈希映射
 * @param {*} str 传入的单个字符串
 */
const hash = (str) => {
  switch (str) {
    case 'A': return 'a'; case 'B': return 'b'; case 'C': return 'c'; case 'D': return 'd'; case 'E': return 'e'; case 'F': return 'f'; case 'G': return 'g'; case 'H': return 'h'; case 'I': return 'i'; case 'J': return 'J'; case 'H': return 'h'; case 'I': return 'i'; case 'J': return 'j'; case 'K': return 'K'; case 'L': return 'l'; case 'M': return 'm'; case 'N': return 'n'; case 'O': return 'o'; case 'P': return 'p'; case 'Q': return 'q'; case 'R': return 'r'; case 'S': return 's'; case 'T': return 't'; case 'U': return 'u'; case 'V': return 'v'; case 'W': return 'w'; case 'X': return 'x'; case 'Y': return 'y'; case 'Z': return 'z'; default : return str;
  }
}

/**
 * @name 转换成小写字母
 * @param {string} str
 * @return {string}
 */
const toLowerCase = (str) => {
  let result = '';
  for (let i = 0; i < str.length; i++) {
    result += hash(str[i]);
  }
  return result;
};
```

Submit 提交：

```js
Accepted
* 8/8 cases passed (68 ms)
* Your runtime beats 32.54 % of javascript submissions
* Your memory usage beats 5.16 % of javascript submissions (34.3 MB)
```

enm...又长又烂，成绩还不好看？

大佬们是怎么实现的，好奇去瞅瞅。

## 六 进一步思考



参考下大佬们的题解，看下有没有收获~

> 利用 ASCII

```js
const toLowerCase = (str) => {
  let result = '';
  for (let i = 0; i < str.length; i++) {
    if (str[i] >= 'A' && str[i] <= 'Z') {
      result += String.fromCharCode(str[i].charCodeAt() + 32);
    } else {
      result += str[i];
    }
  }
  return result;
};
```

Submit 提交：

```js
Accepted
* 8/8 cases passed (68 ms)
* Your runtime beats 32.54 % of javascript submissions
* Your memory usage beats 5.16 % of javascript submissions (34.4 MB)
```

如果小伙伴们有更好的思路或者想法，欢迎评论留言或者直接私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

