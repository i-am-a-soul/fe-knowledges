1025 - 除数博弈（divisor-game）
===

> Create by **jsliang** on **2020-01-30 10:28:15**  
> Recently revised in **2020-01-30 11:22:55**

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
* **涉及知识**：数学、动态规划
* **题目地址**：https://leetcode-cn.com/problems/divisor-game/
* **题目内容**：

```
爱丽丝和鲍勃一起玩游戏，
他们轮流行动。
爱丽丝先手开局。

最初，黑板上有一个数字 N 。
在每个玩家的回合，玩家需要执行以下操作：

选出任一 x，满足 0 < x < N 且 N % x == 0 。
用 N - x 替换黑板上的数字 N 。
如果玩家无法执行这些操作，就会输掉游戏。

只有在爱丽丝在游戏中取得胜利时才返回 True，
否则返回 false。假设两个玩家都以最佳状态参与游戏。

示例 1：

输入：2
输出：true
解释：爱丽丝选择 1，鲍勃无法进行操作。

示例 2：

输入：3
输出：false
解释：爱丽丝选择 1，鲍勃也选择 1，然后爱丽丝无法进行操作。
 
提示：

1 <= N <= 1000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/divisor-game
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} N
 * @return {boolean}
 */
var divisorGame = function(N) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 除数博弈
 * @param {number} N
 * @return {boolean}
 */
const divisorGame = (N) => {
  return N % 2 === 0;
};

console.log(divisorGame(2)); // true
console.log(divisorGame(3)); // false
```

`node index.js` 返回：

```js
true
false
```

## 四 LeetCode Submit



```js
Accepted
* 40/40 cases passed (64 ms)
* Your runtime beats 62.69 % of javascript submissions
* Your memory usage beats 83.73 % of javascript submissions (33.7 MB)
```

## 五 解题思路



我感觉这是一道找规律题啊，先摸清敌情：

```
【√】2 -> 1
【X】3
【√】4 -> 1
【X】5
【√】6 -> 1
【X】7
【√】8 -> 1
【x】9
【√】10 -> 1
【X】11
【X】12 -> 1
【X】13
【√】14 -> 1
【X】15

不行：3 5 7 9 11 13 15
```

enm...判断奇偶数？这么简单？！

> 暴力破解

```js
const divisorGame = (N) => {
  return N % 2 === 0;
};
```

Submit 提交：

```js
Accepted
* 40/40 cases passed (64 ms)
* Your runtime beats 62.69 % of javascript submissions
* Your memory usage beats 83.73 % of javascript submissions (33.7 MB)
```

enm......

真没啥花里胡哨的~

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

