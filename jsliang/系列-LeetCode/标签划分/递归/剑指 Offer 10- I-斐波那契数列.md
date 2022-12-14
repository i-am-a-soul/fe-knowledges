剑指 Offer 10- I - 斐波那契数列
===

> Create by **jsliang** on **2020-08-07 14:47:58**  
> Recently revised in **2020-08-07 14:57:33**

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
写一个函数，输入 n ，
求斐波那契（Fibonacci）数列的第 n 项。

斐波那契数列的定义如下：
* F(0) = 0,
* F(1) = 1
* F(N) = F(N - 1) + F(N - 2), 其中 N > 1.

斐波那契数列由 0 和 1 开始，
之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），
如计算初始结果为：1000000008，请返回 1。 

示例 1：
输入：n = 2
输出：1

示例 2：
输入：n = 5
输出：5

提示：

0 <= n <= 100
注意：本题与主站 509 题相同：https://leetcode-cn.com/problems/fibonacci-number/

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```js
/**
 * @param {number} n
 * @return {number}
 */
var fib = function(n) {

};
```

根据上面的已知函数，小伙伴们可以先尝试破解本题，确定了自己的答案后再看下面代码。

## 三 解题思路



* 递归（爆栈）

```js
/**
 * @param {number} n
 * @return {number}
 */
const fib = (n) => {
  if (n <= 1) {
    return n;
  }
  return fib(n - 1) + fib(n - 2);
};

console.log(fib(100)); // 687995182
```

* 递归（优化）

```js
/**
 * @param {number} n
 * @return {number}
 */
const fib = (n, map = [0, 1]) => {
  if (map[n] !== undefined) {
    return map[n];
  }
  map[n] = (fib(n - 1, map) + fib(n - 2, map)) % 1000000007;
  return map[n];
};

console.log(fib(100)); // 687995182
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

