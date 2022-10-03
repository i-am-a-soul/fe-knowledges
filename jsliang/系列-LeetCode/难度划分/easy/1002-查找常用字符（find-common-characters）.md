1002 - 查找常用字符（find-common-characters）
===

> Create by **jsliang** on **2020-01-29 15:31:06**  
> Recently revised in **2020-01-29 16:19:52**

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
* **题目地址**：https://leetcode-cn.com/problems/find-common-characters/
* **题目内容**：

```
给定仅有小写字母组成的字符串数组 A，
返回列表中的每个字符串中都显示的全部字符（包括重复字符）组成的列表。

例如，如果一个字符在每个字符串中出现 3 次，
但不是 4 次，则需要在最终答案中包含该字符 3 次。

你可以按任意顺序返回答案。

示例 1：

输入：["bella","label","roller"]
输出：["e","l","l"]

示例 2：

输入：["cool","lock","cook"]
输出：["c","o"]
 
提示：

1 <= A.length <= 100
1 <= A[i].length <= 100
A[i][j] 是小写字母

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-common-characters
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string[]} A
 * @return {string[]}
 */
var commonChars = function(A) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 查找常用字符
 * @param {string[]} A
 * @return {string[]}
 */
const commonChars = (A) => {
  return A.map(item => item.split('')).reduce((prev, next) => {
    return prev.filter(item => {
      const index = next.indexOf(item);
      if (index > -1) {
        next.splice(index, 1);
        return true;
      }
      return false;
    });
  });
};

console.log(commonChars(['bella', 'label', 'roller'])); // ['e', 'l', 'l']
console.log(commonChars(['cool', 'lock', 'cook'])); // ['c', 'o']
```

`node index.js` 返回：

```js
[ 'e', 'l', 'l' ]
[ 'c', 'o' ]
```

## 四 LeetCode Submit



```js
Accepted
* 83/83 cases passed (72 ms)
* Your runtime beats 92.73 % of javascript submissions
* Your memory usage beats 63.05 % of javascript submissions (37.4 MB)
```

## 五 解题思路



题目很简洁，稍微理解下应该能分析到题意：

```
示例 1：

输入：["bella","label","roller"]
输出：["e","l","l"]

示例 2：

输入：["cool","lock","cook"]
输出：["c","o"]
```

意思即是：

1. 统计在每个字段中都出现的字符；
2. 如果出现多次，则显示多次。

简单来说：

* 开心消消乐

那么，开始游戏：

> 暴力破解

```js
const commonChars = (A) => {
  return A.map(item => item.split('')).reduce((prev, next) => {
    return prev.filter(item => {
      const index = next.indexOf(item);
      if (index > -1) {
        next.splice(index, 1);
        return true;
      }
      return false;
    });
  });
};
```

1. 通过 `A.map()` 返回一个新数组，将 A 里面所有字符串元素转换成数组。
2. 通过 `A.map().reduce()` 进行累加操作，这个累加，是通过前后的对比进行合计。例如有 `['bella', 'label', 'roller']`，那么第一次是 `bella` 和 `label` 进行比对，留下 `b, e, l, l, a`；第二次是 `b, e, l, l, a` 和 `roller` 比对，留下 `e, l, l`。
3. 通过 `prev.filter()` 过滤它和 `next` 中相同的每一项。本来打算用 `has` 直接过滤取交集的，发现它不能过滤重复出现的元素，只要手动操作了。

Submit 提交：

```js
Accepted
* 83/83 cases passed (72 ms)
* Your runtime beats 92.73 % of javascript submissions
* Your memory usage beats 63.05 % of javascript submissions (37.4 MB)
```

还是挺不错的~

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

