1160 - 拼写单词（find-words-that-can-be-formed-by-characters）
===

> Create by **jsliang** on **2020-01-31 15:20:21**  
> Recently revised in **2020-01-31 17:16:01**

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
* **涉及知识**：数组、哈希表
* **题目地址**：https://leetcode-cn.com/problems/find-words-that-can-be-formed-by-characters/
* **题目内容**：

```
给你一份『词汇表』（字符串数组） words，
和一张『字母表』（字符串） chars。

假如你可以用 chars 中的『字母』（字符），
拼写出 words 中的某个『单词』（字符串），
那么我们就认为你掌握了这个单词。

注意：每次拼写时，chars 中的每个字母都只能用一次。

返回词汇表 words 中你掌握的所有单词的 长度之和。

示例 1：

输入：
words = ["cat","bt","hat","tree"],
chars = "atach"
输出：6
解释： 
可以形成字符串 "cat" 和 "hat"，所以答案是 3 + 3 = 6。

示例 2：

输入：
words = ["hello","world","leetcode"],
chars = "welldonehoneyr"
输出：10
解释：
可以形成字符串 "hello" 和 "world"，所以答案是 5 + 5 = 10。

提示：

1 <= words.length <= 1000
1 <= words[i].length, chars.length <= 100
所有字符串中都仅包含小写英文字母

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-words-that-can-be-formed-by-characters
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string[]} words
 * @param {string} chars
 * @return {number}
 */
var countCharacters = function(words, chars) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 拼写单词
 * @param {string[]} words
 * @param {string} chars
 * @return {number}
 */
const countCharacters = (words, chars) => {
  chars = chars.split('');
  let result = 0;
  for (let i = 0; i < words.length; i++) {
    let flag = true;
    const word = words[i].split('');
    for (let j = 0; j < word.length; j++) {
      const length1 = word.filter(item => item === word[j]).length;
      const length2 = chars.filter(item => item === word[j]).length;
      if (length1 > length2) {
        flag = false;
        break;
      }
    }
    if (flag) {
      result += word.length;
    }
  }
  return result;
};

console.log(countCharacters(['cat', 'bt', 'hat', 'tree'], 'atach')); // 6
console.log(countCharacters(['hello', 'world', 'leetcode'], 'welldonehoneyr')); // 10
```

`node index.js` 返回：

```js
6
10
```

## 四 LeetCode Submit



```js
Accepted
* 36/36 cases passed (204 ms)
* Your runtime beats 61.29 % of javascript submissions
* Your memory usage beats 67.35 % of javascript submissions (43.5 MB)
```

## 五 解题思路



先看懂题目意思：

1. 给定一份词汇表 `words` 和一份字母表 `chars`。
2. 判断 `chars` 是否能构成 `words` 中的词汇。
3. 字母表 `chars` 中的字母在对同一个词汇中只能使用一次。
4. 返回能构成词汇的长度和。

示例：

> 示例 1

```
输入：
words = ['cat', 'bt', 'hat', 'tree']
chars = 'atach'

输出：6

解释：
能够组成 'cat' 和 'hat' 两个字符串，长度为 3 + 3 = 6
```

> 示例 2

```
输入：
words = ['hello', 'world', 'leetcode']
chars = 'welldonehoneyr'

输出：10

解释：
能够组成 'hello' 和 'world' 连个字符串，长度为 5 + 5 = 10
```

OK，开始解题：

> 暴力破解

```js
const countCharacters = (words, chars) => {
  chars = chars.split('');
  let result = 0;
  for (let i = 0; i < words.length; i++) {
    let flag = true;
    const word = words[i].split('');
    for (let j = 0; j < word.length; j++) {
      const length1 = word.filter(item => item === word[j]).length;
      const length2 = chars.filter(item => item === word[j]).length;
      if (length1 > length2) {
        flag = false;
        break;
      }
    }
    if (flag) {
      result += word.length;
    }
  }
  return result;
};
```

如果我没记错的话，类似的题目出现过挺多次了，求字符串 `a` 和字符串 `b` 是否包含共有字母或者字符串 `a` 是否为字符串 `b` 的子集之类的。

这道题求的就是字符串 `a` 是否为字符串 `b` 的子集。

那么就有思路：

1. 先将 `chars` 打成数组，以及 `words` 中的每个元素打成数组。
2. 然后判断 `words` 中每个元素的每个字母，看它在 `words[i]` 中的长度和 `chars` 中的长度比对。如果 `chars.length` 满足不了它的要求，那么 `flag` 红牌直接给出即可。
3. 如果满足了要求，那么 `result` 加上这个长度，最终返回这个长度接口。

写上面思路的时候，突然想起如果红牌都给了，就没必要继续遍历字符串了。

所以有：

```js
if (length1 > length2) {
  flag = false;
  break;
}
```

小伙伴可能疑问这有没有作用，可以对比下：

> break 前

```js
Accepted
* 36/36 cases passed (3028 ms)
* Your runtime beats 5.38 % of javascript submissions
* Your memory usage beats 54.42 % of javascript submissions (44 MB)
```

> break 后

```js
Accepted
* 36/36 cases passed (204 ms)
* Your runtime beats 61.29 % of javascript submissions
* Your memory usage beats 67.35 % of javascript submissions (43.5 MB)
```

OK，这样，我们就完成了这道题的破解。

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

