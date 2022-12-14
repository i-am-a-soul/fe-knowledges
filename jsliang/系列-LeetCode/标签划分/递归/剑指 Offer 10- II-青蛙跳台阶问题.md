剑指 Offer 10- II - 青蛙跳台阶问题
===

> Create by **jsliang** on **2020-08-05 16:47:20**  
> Recently revised in **2020-08-05 17:02:38**

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- |
| [一 目录](#chapter-one) |
| [二 题目](#chapter-two) |
| [三 解题思路](#chapter-three) |
| [四 解题套路](#chapter-four) |

## 二 题目



```
一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。
求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），
如计算初始结果为：1000000008，请返回 1。

示例 1：
输入：n = 2
输出：2

示例 2：
输入：n = 7
输出：21

示例 3：
输入：n = 0
输出：1

提示：
0 <= n <= 100

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```js
/**
 * @param {number} n
 * @return {number}
 */
const numWays = (n) => {

};
```

根据上面的已知函数，小伙伴们可以先尝试破解本题，确定了自己的答案后再看下面代码。

## 三 解题思路



思考：

* 能否找到规律？

```
0 -> 1 -> 强制
1 -> 1 -> 只跳 1 阶
2 -> 2 -> 可以跳 1+1 阶或者 2 阶
3 -> 3 -> 可跳：1+1+1、1+2、2+1
4 -> 5 -> 可跳：1+1+1+1、1+1+2、1+2+1、2+1+1、2+2
……以此类推
```

这莫非，是斐波那契数列？再看题目：

* 答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

意思是普通的递归是不可取的，会爆栈。

所以咱们直接上优化版递归：

```js
/**
 * @param {number} n
 * @return {number}
 */
const numWays = (n, map = [1, 1, 2]) => {
  if (map[n]) {
    return map[n];
  }
  map[n] = (numWays(n - 1, map) + numWays(n - 2, map)) % 1000000007;
  return map[n];
};

console.log(numWays(100)); // 21
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

