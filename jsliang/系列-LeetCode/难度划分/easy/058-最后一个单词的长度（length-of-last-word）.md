058 - 最后一个单词的长度（length-of-last-word）
===

> Create by **jsliang** on **2019-06-10 18:18:16**  
> Recently revised in **2019-09-18 10:18:22**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| &emsp;[3.1 解题 - 暴力破解](#chapter-three-one) |
| &emsp;[3.2 解法 - 正则表达式](#chapter-three-two) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：字符串
* **题目地址**：https://leetcode-cn.com/problems/length-of-last-word/
* **题目内容**：

```
给定一个仅包含大小写字母和空格 ' ' 的字符串，返回其最后一个单词的长度。

如果不存在最后一个单词，请返回 0 。

说明：一个单词是指由字母组成，但不包含任何空格的字符串。

示例:
输入: "Hello World"
输出: 5
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 讲解下使用 JavaScript 的解题思路。

### <a name="chapter-three-one" id="chapter-three-one">3.1 解法 - 暴力破解</a>



* **解题代码**：

```js
var lengthOfLastWord = function(s) {
  // 防止 'b   a  cc' 的情况，去掉多余空格（去重）
  const result = [...new Set(s.split(' '))];
  // 防止 'a  ' 的情况
  if (result.length >=2 && result[result.length - 1] === '') {
    return result[result.length - 2].length
  }
  return result[result.length - 1].length;
};
```

* **执行测试**：

1. `s`：`Hello World`
2. `return`：

```js
5
```

* **LeetCode Submit**：

```js
✔ Accepted
  ✔ 59/59 cases passed (72 ms)
  ✔ Your runtime beats 96.22 % of javascript submissions
  ✔ Your memory usage beats 20.38 % of javascript submissions (33.9 MB)
```

* **知识点**：

1. `split()`：`split()` 方法使用指定的分隔符字符串将一个 String 对象分割成字符串数组，以将字符串分隔为子字符串，以确定每个拆分的位置。[`split()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/String/split.md)
2. `Set`：`Set` 对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用。[`Set` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Set/README.md)

* **解题思路**：

**首先**，说个比较复杂的逻辑：

1. 通过 `split()` 将字符串打成数组
2. 通过 `Set` 对数组去重
3. 通过 `[...Object]` 扩展运算符再将 `Set` 类型打成数组。

**然后**，由于 `'a '` 的情况下，会将该字符串转成 `['a', '']`，所以我们需要判断最后一个是不是 `''`，如果是的话，我们取倒数第二个的长度。

**最后**，正常情况下，返回倒数第一个的长度。

### <a name="chapter-three-two" id="chapter-three-two">3.2 解法 - 正则表达式</a>



* **解题代码**：

```js
var lengthOfLastWord = function(s) {
  s = s.replace(/(\s*$)/g, "");
  let arr = s.split(' ');
  return arr[arr.length - 1].length;
};
```

* **执行测试**：

1. `s`：`Hello World`
2. `return`：

```js
5
```

* **LeetCode Submit**：

```js
✔ Accepted
  ✔ 59/59 cases passed (64 ms)
  ✔ Your runtime beats 99.42 % of javascript submissions
  ✔ Your memory usage beats 35.25 % of javascript submissions (33.7 MB)
```

* **知识点**：

1. `RegExp`：构造函数的原型对象。常用语一些便捷操作。[`RegExp` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/RegExp/README.md)
2. `split()`：`split()` 方法使用指定的分隔符字符串将一个 String 对象分割成字符串数组，以将字符串分隔为子字符串，以确定每个拆分的位置。[`split()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/String/split.md)

* **解题思路**：

**首先**，进行正则去空格，`\s` 的意思是匹配任何空白字符，包括空格、制表符、换行符等，而 `*` 表示任意个，`$` 表示结尾，所以 `\s*$` 的意思就是匹配结尾的任意个空格，并将其替换为 `''`（注意，不是空，而是去掉）

**然后**，通过 `split()` 将字符串打成数组。

**最后**，返回数组最后一位的长度。

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

