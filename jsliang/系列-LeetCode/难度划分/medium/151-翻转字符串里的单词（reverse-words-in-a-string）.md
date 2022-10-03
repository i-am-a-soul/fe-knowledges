面试题03 - 数组中重复的数字
===

> Create by **jsliang** on **2020-07-02 19:17:03**  
> Recently revised in **2020-07-02 19:18:09**  

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- |
| [一 目录](#chapter-one) |
| [二 题目](#chapter-two) |
| [三 解题思路](#chapter-three) |
| [四 统计分析](#chapter-four) |
| [五 解题套路](#chapter-five) |

## 二 题目



```
给定一个字符串，逐个翻转字符串中的每个单词。

示例 1：

输入: "the sky is blue"
输出: "blue is sky the"

示例 2：

输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。

示例 3：

输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。

说明：

无空格字符构成一个单词。
输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。

进阶：

请选用 C 语言的用户尝试使用 O(1) 额外空间复杂度的原地解法。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reverse-words-in-a-string
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```js
/**
 * @param {string} s
 * @return {string}
 */
var reverseWords = function(s) {

};
```

根据上面的已知函数，小伙伴们可以先尝试破解本题，确定了自己的答案后再看下面代码。

## 三 解题思路



按道理属于简单题：

```js
const reverseWords = (s) => {
  const arr = s.trim().split(' ').reverse();
  let result = arr[0];
  for (let i = 1; i < arr.length; i++) {
    if (arr[i]) {
      result += ' ' + arr[i];
    }
  }
  return result;
};
```

## 四 统计分析



本题不需要统计分析。

## 五 套路分析



本题暂未发现任何套路，如果有但是 **jsliang** 后面发现了的话，会在 GitHub 进行补充。

如果小伙伴有更好的思路想法，或者没看懂其中某种解法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](https://github.com/LiangJunrong/document-library/blob/master/public-repertory/img/z-index-small.png?raw=true)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

