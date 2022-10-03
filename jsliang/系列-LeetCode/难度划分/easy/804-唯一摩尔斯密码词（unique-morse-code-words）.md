804 - 唯一摩尔斯密码词（unique-morse-code-words）
===

> Create by **jsliang** on **2020-01-05 11:18:08**  
> Recently revised in **2020-01-05 11:44:46**

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
* **题目地址**：https://leetcode-cn.com/problems/unique-morse-code-words/
* **题目内容**：

```
国际摩尔斯密码定义一种标准编码方式，
将每个字母对应于一个由一系列点和短线组成的字符串，
比如: "a" 对应 ".-", 
"b" 对应 "-...",
"c" 对应 "-.-.", 等等。

为了方便，所有26个英文字母对应摩尔斯密码表如下：

[
  ".-","-...","-.-.","-..",
  ".","..-.","--.","....",
  "..",".---","-.-",".-..",
  "--","-.","---",".--.",
  "--.-",".-.","...","-",
  "..-","...-",".--","-..-",
  "-.--","--.."
]

给定一个单词列表，
每个单词可以写成每个字母对应摩尔斯密码的组合。

例如，"cab" 可以写成 "-.-..--..."，
(即 "-.-." + "-..." + ".-"字符串的结合)。
我们将这样一个连接过程称作单词翻译。

返回我们可以获得所有词不同单词翻译的数量。

例如:
输入: words = ["gin", "zen", "gig", "msg"]
输出: 2
解释: 
各单词翻译如下:
"gin" -> "--...-."
"zen" -> "--...-."
"gig" -> "--...--."
"msg" -> "--...--."

共有 2 种不同翻译, "--...-." 和 "--...--.".

注意:

单词列表 words 的长度不会超过 100。
每个单词 words[i]的长度范围为 [1, 12]。
每个单词 words[i]只包含小写字母。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string[]} words
 * @return {number}
 */
var uniqueMorseRepresentations = function(words) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 转换单词为摩尔斯密码
 * @param {*} word 
 */
const transform = (word) => {
  let str = '';
  const map = ['.-', '-...', '-.-.', '-..', '.', '..-.', '--.', '....', '..', '.---', '-.-', '.-..', '--', '-.', '---', '.--.', '--.-', '.-.', '...', '-', '..-', '...-', '.--', '-..-', '-.--', '--..']
  for (let i = 0; i < word.length; i++) {
    str += map[word[i].charCodeAt() - 97];
  }
  return str;
};

/**
 * @name 唯一摩尔斯密码词
 * @param {string[]} words
 * @return {number}
 */
const uniqueMorseRepresentations = (words) => {
  const result = [];
  for (let i = 0; i < words.length; i++) {
    result.push(transform(words[i]));
  }
  return [...new Set(result)].length;
};

console.log(uniqueMorseRepresentations(['gin', 'zen', 'gig', 'msg']));
```

`node index.js` 返回：

```js
2
```

## 四 LeetCode Submit



```js
Accepted
* 83/83 cases passed (76 ms)
* Your runtime beats 42.39 % of javascript submissions
* Your memory usage beats 20.64 % of javascript submissions (35.7 MB)
```

## 五 解题思路



小意思啦，直接解题：

> 暴力破解

```js
const transform = (word) => {
  let str = '';
  const map = ['.-', '-...', '-.-.', '-..', '.', '..-.', '--.', '....', '..', '.---', '-.-', '.-..', '--', '-.', '---', '.--.', '--.-', '.-.', '...', '-', '..-', '...-', '.--', '-..-', '-.--', '--..']
  for (let i = 0; i < word.length; i++) {
    str += map[word[i].charCodeAt() - 97];
  }
  return str;
};

const uniqueMorseRepresentations = (words) => {
  const result = [];
  for (let i = 0; i < words.length; i++) {
    result.push(transform(words[i]));
  }
  return [...new Set(result)].length;
};
```

为了代码看起来简洁，所以抽取了一个方法 `transform`，主要功能是将单词转换成摩尔斯密码词。

最后通过 `Set` 去重得到 `length` 长度即可。

Submit 提交如下：

```js
Accepted
* 83/83 cases passed (76 ms)
* Your runtime beats 42.39 % of javascript submissions
* Your memory usage beats 20.64 % of javascript submissions (35.7 MB)
```

## 六 进一步思考



当然，还有其他法子：

> 优化：哈希表

```js
const uniqueMorseRepresentations = (words) => {
  const map = new Map();
  const hash = ['.-', '-...', '-.-.', '-..', '.', '..-.', '--.', '....', '..', '.---', '-.-', '.-..', '--', '-.', '---', '.--.', '--.-', '.-.', '...', '-', '..-', '...-', '.--', '-..-', '-.--', '--..'];
  for (let i = 0; i < words.length; i++) {
    let tempStr = '';
    for (let j = 0; j < words[i].length; j++) {
      tempStr += hash[words[i][j].charCodeAt() - 97];
    }
    map.set(tempStr, tempStr);
  }
  return map.size;
};
```

当然，很奇怪的是，它的效率跟前面都是半桶水啦：

```js
Accepted
* 83/83 cases passed (76 ms)
* Your runtime beats 42.39 % of javascript submissions
* Your memory usage beats 17.99 % of javascript submissions (35.8 MB)
```

如果你有更好的思路或者想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

