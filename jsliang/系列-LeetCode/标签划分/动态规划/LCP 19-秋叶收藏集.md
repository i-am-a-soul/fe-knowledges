LCP 19 - 秋叶收藏集
===

> Create by **jsliang** on **2020-10-01 09:41:47**  
> Recently revised in **2020-10-01 10:24:00**

<!-- 目录开始 -->
## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- |
| [一 目录](#chapter-one) |
| [二 题目](#chapter-two) |
| [三 解题思路](#chapter-three) |
| [四 解题套路](#chapter-four) |
<!-- 目录结束 -->

## 二 题目



```
小扣出去秋游，途中收集了一些红叶和黄叶。

他利用这些叶子初步整理了一份秋叶收藏集 leaves，
字符串 leaves 仅包含小写字符 r 和 y，
其中字符 r 表示一片红叶，字符 y 表示一片黄叶。

出于美观整齐的考虑，小扣想要将收藏集中树叶的排列调整成「红、黄、红」三部分。

每部分树叶数量可以不相等，但均需大于等于 1。

每次调整操作，
小扣可以将一片红叶替换成黄叶或者将一片黄叶替换成红叶。

请问小扣最少需要多少次调整操作才能将秋叶收藏集调整完毕。

示例 1：

输入：leaves = "rrryyyrryyyrr"
输出：2
解释：调整两次，将中间的两片红叶替换成黄叶，得到 "rrryyyyyyyyrr"

示例 2：

输入：leaves = "ryr"
输出：0
解释：已符合要求，不需要额外操作

提示：

3 <= leaves.length <= 10^5
leaves 中只包含字符 'r' 和字符 'y'

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/UlBDOe
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```js
/**
 * @param {string} leaves
 * @return {number}
 */
var minimumOperations = function(leaves) {

};
```

根据上面的已知函数，小伙伴们可以先尝试破解本题，确定了自己的答案后再看下面代码。

## 三 解题思路



```js
/**
 * @param {string} leaves
 * @return {number}
 */
const minimumOperations = (leaves) => {
  // 初始状态不可能为 2, 3，设置为 Infinity
  let dp = [leaves[0] === 'r' ? 0 : 1, Infinity, Infinity];

  for (let i = 1; i < leaves.length; i++) {
    const isRed = leaves[i] === 'r';
    dp = [
      dp[0] + (isRed ? 0 : 1),
      Math.min(dp[0], dp[1]) + (isRed ? 1 : 0),
      Math.min(dp[1], dp[2]) + (isRed ? 0 : 1),
    ];
  }

  return dp[2];
};

/*
  rryyrr -> 符合
  rryyryyr -> rryyyyyr -> 中间变更 1 次
  yyyrr -> ryyrr -> 左边变更 1 次
  rryyy -> rryyr -> 右边变更 1 次
  rryyrrryrr -> rryyrrrrrr -> 中间变更 1 次
  rryrrryyrr -> rrrrrryyrr -> 中间变更 1 次
*/

// console.log(minimumOperations('rrryyyrryyyrr')); // 'rrryyyyyyyyrr' -> 2
console.log(minimumOperations('yyrryyrryyrryy')); // 'rrrryyyyyyrrrr' -> 6
```

## 四 套路分析



本题暂未发现任何套路，如果有但是 **jsliang** 后面发现了的话，会在 GitHub 进行补充。

如果小伙伴有更好的思路想法，或者没看懂其中某种解法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](https://github.com/LiangJunrong/document-library/blob/master/public-repertory/img/z-index-small.png?raw=true)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

