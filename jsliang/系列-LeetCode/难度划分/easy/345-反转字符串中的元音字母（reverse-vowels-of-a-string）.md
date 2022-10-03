345 - 反转字符串中的元音字母（reverse-vowels-of-a-string）
===

> Create by **jsliang** on **2019-7-23 08:08:54**  
> Recently revised in **2019-09-18 13:54:16**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| [四 执行测试](#chapter-four) |
| [五 LeetCode Submit](#chapter-five) |
| [六 知识点](#chapter-six) |
| [七 解题思路](#chapter-seven) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：双指针、字符串
* **题目地址**：https://leetcode-cn.com/problems/reverse-vowels-of-a-string/
* **题目内容**：

```
编写一个函数，以字符串作为输入，反转该字符串中的元音字母。

示例 1:
输入: "hello"
输出: "holle"

示例 2:
输入: "leetcode"
输出: "leotcede"

说明:
元音字母不包含字母"y"。
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var reverseVowels = function(s) {
  s = s.split('');
  let i = 0;
  let j = s.length - 1;
  let vowers = ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'];
  while (i < j) {
    if (!vowers.includes(s[i])) {
      i++;
      continue;
    }
    if (!vowers.includes(s[j])) {
      j--;
      continue;
    }
    [s[i], s[j]] = [s[j], s[i]];
    i++;
    j--;
  }
  return s.join('');
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



1. `s`：`hello`
2. `return`：

```js
holle
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
√ Accepted
  √ 481/481 cases passed (112 ms)
  √ Your runtime beats 85.51 % of javascript submissions
  √ Your memory usage beats 59.65 % of javascript submissions (38.6 MB)
```

## <a name="chapter-six" id="chapter-six">六 知识点</a>



1. `split()`：`split()` 方法使用指定的分隔符字符串将一个 String 对象分割成字符串数组，以将字符串分隔为子字符串，以确定每个拆分的位置。[`split()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/String/split.md)
2. `join()`：`join()` 方法将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。[`join()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Array/join.md)

## <a name="chapter-seven" id="chapter-seven">七 解题思路</a>



**首先**，看到 “元音字母”，脑海里回应出：`a e i o u`。

OK，然后再看看题目，应该是 **双指针** 了，立马写出第一印象的题解：

> 这里讲解从 0 到 1 的思路，而不是直接上最终解

```js
// vowel - 元音字母
// letter - 字母
const vowel = (letter) => {
  if (letter === 'a'
  || letter === 'e'
  || letter === 'i'
  || letter === 'o'
  || letter === 'u') {
    return true;
  }
  return false;
}

var reverseVowels = function(s) {
  s = s.split('');
  for (let i = 0; i < (s.length - 1) / 2; i++) {
    for (let j = s.length - 1; j > (s.length - 1) / 2; j--) {
      if (vowel(s[i]) && vowel(s[j])) {
        let temp = s[j];
        s[j] = s[i];
        s[i] = temp;
        i++;
      }
    }
  }
  return s.join('');
};
```

所以它就报错了，告诉我 `aA` 应该变成 `Aa`：

```js
× Wrong Answer
  × 88/481 cases passed (N/A)
  × testcase: '"aA"'
  × answer: "aA"
  × expected_answer: "Aa"
  × stdout:
```

想想后面还有近 400 个测试用例，赶紧改回来：

```js
const vowel = (letter) => {
  if (letter === 'a'
  || letter === 'A'
  || letter === 'e'
  || letter === 'E'
  || letter === 'i'
  || letter === 'I'
  || letter === 'o'
  || letter === 'O'
  || letter === 'u'
  || letter === 'U') {
    return true;
  }
  return false;
}
```

再 Submit，它就告诉我，错了：

```js
× Wrong Answer
  × 90/481 cases passed (N/A)
  × testcase: '"A man, a plan, a canal: Panama"'
  × answer: "a mAn, a plan, a canal: Panama"
  × expected_answer: "a man, a plan, a canal: PanamA"
  × stdout:
```

那么我想是不是 `for` 循环不太理想？该 `while` 试试：

```js
const vowel = (letter) => {
  if (letter === 'a'
  || letter === 'A'
  || letter === 'e'
  || letter === 'E'
  || letter === 'i'
  || letter === 'I'
  || letter === 'o'
  || letter === 'O'
  || letter === 'u'
  || letter === 'U') {
    return true;
  }
  return false;
}

var reverseVowels = function(s) {
  s = s.split('');
  let i = 0;
  let j = s.length - 1;
  while (i < j) {
    if (!vowel(s[i])) {
      i++;
      continue;
    }
    if (!vowel(s[j])) {
      j--;
      continue;
    }
    [s[i], s[j]] = [s[j], s[i]];
    i++;
    j--;
  }
  return s.join('');
};
```

Submit 提交看看：

```js
√ Accepted
  √ 481/481 cases passed (116 ms)
  √ Your runtime beats 79.71 % of javascript submissions
  √ Your memory usage beats 82.46 % of javascript submissions (38 MB)
```

nice~顺带看看大佬的题解，优化下自己的代码：

```js
var reverseVowels = function(s) {
  s = s.split('');
  let i = 0;
  let j = s.length - 1;
  let vowers = ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'];
  while (i < j) {
    if (!vowers.includes(s[i])) {
      i++;
      continue;
    }
    if (!vowers.includes(s[j])) {
      j--;
      continue;
    }
    [s[i], s[j]] = [s[j], s[i]];
    i++;
    j--;
  }
  return s.join('');
};
```

很好，这样我们就完成了这道题的题解啦~

> 如果小伙伴有兴趣，可以尝试其他解法哈~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

