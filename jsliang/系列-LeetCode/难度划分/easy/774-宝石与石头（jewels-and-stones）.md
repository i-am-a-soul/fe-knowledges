774 - 宝石与石头（jewels-and-stones）
===

> Create by **jsliang** on **2020-01-04 08:38:32**  
> Recently revised in **2020-01-04 08:59:47**

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
* **涉及知识**：哈希表
* **题目地址**：https://leetcode-cn.com/problems/jewels-and-stones/
* **题目内容**：

```
给定字符串 J 代表石头中宝石的类型，
和字符串 S 代表你拥有的石头。

S 中每个字符代表了一种你拥有的石头的类型，
你想知道你拥有的石头中有多少是宝石。

J 中的字母不重复，
J 和 S 中的所有字符都是字母。
字母区分大小写，
因此 "a" 和 "A" 是不同类型的石头。

示例 1:

输入: J = "aA", S = "aAAbbbb"
输出: 3

示例 2:

输入: J = "z", S = "ZZ"
输出: 0

注意:

S 和 J 最多含有50个字母。
 J 中的字符不重复。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} J
 * @param {string} S
 * @return {number}
 */
var numJewelsInStones = function(J, S) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 宝石与石头
 * @param {string} J
 * @param {string} S
 * @return {number}
 */
const numJewelsInStones = (J, S) => {
  const map = new Map();
  for (let i = 0; i < J.length; i++) {
    map.set(J[i], true);
  }
  let result = 0;
  for (let i = 0; i < S.length; i++) {
    if (map.get(S[i])) {
      result += 1;
    }
  }
  return result;
};

console.log(numJewelsInStones('aA', 'aAAbbbb')); // 3
console.log(numJewelsInStones('z', 'ZZ')); // 0
```

`node index.js` 返回：

```js
3
0
```

## 四 LeetCode Submit



```js
Accepted
* 254/254 cases passed (68 ms)
* Your runtime beats 70.91 % of javascript submissions
* Your memory usage beats 31.24 % of javascript submissions (34.4 MB)
```

## 五 解题思路



太过简单，都懒得思考了，直接撸代码：

> 哈希表

```js
const numJewelsInStones = (J, S) => {
  const map = new Map();
  for (let i = 0; i < J.length; i++) {
    map.set(J[i], true);
  }
  let result = 0;
  for (let i = 0; i < S.length; i++) {
    if (map.get(S[i])) {
      result += 1;
    }
  }
  return result;
};
```

定义一个哈希表，记录 `J` 的所有内容。

然后遍历 `S` 的所有内容，如果其中的元素是哈希表中出现的，那么就将结果 `result + 1`。

Submit 提交如下：

```js
Accepted
* 254/254 cases passed (68 ms)
* Your runtime beats 70.91 % of javascript submissions
* Your memory usage beats 31.24 % of javascript submissions (34.4 MB)
```

值得思考，自秤是比较精炼的了，居然效率那么低下？

换一种题解：

> 暴力破解

```js
const numJewelsInStones = (J, S) => {
  let result = 0;
  for (let i = 0; i < S.length; i++) {
    if (J.includes(S[i])) {
      result += 1;
    }
  }
  return result;
};
```

Submit 提交：

```js
Accepted
* 254/254 cases passed (72 ms)
* Your runtime beats 50.38 % of javascript submissions
* Your memory usage beats 76.38 % of javascript submissions (33.7 MB)
```

enm...还是不如人意？

所以大佬做了啥，居然给刷得那么厉害。

> 一行求解

```js
const numJewelsInStones = (J, S) => S.split('').filter(i => J.includes(i)).length;
```

Submit 提交：

```js
Accepted
* 254/254 cases passed (64 ms)
* Your runtime beats 85.15 % of javascript submissions
* Your memory usage beats 37.81 % of javascript submissions (34.3 MB)
```

越发在意，存储（memory）的占用都那么少，时间（runtime）也不是很好……

在【题解区】和【评论区】找了很久，发觉不是事儿，指不定大佬做完，也没有 show 一下解析。

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

