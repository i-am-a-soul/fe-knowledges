50 - Pow(x, n)
===

> Create by **jsliang** on **2020-08-07 17:45:29**  
> Recently revised in **2020-08-07 17:47:10**

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
实现 pow(x, n) ，即计算 x 的 n 次幂函数。

示例 1:
输入: 2.00000, 10
输出: 1024.00000

示例 2:
输入: 2.10000, 3
输出: 9.26100

示例 3:
输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25

说明:
* -100.0 < x < 100.0
* n 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/powx-n
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```js
/**
 * @param {number} x
 * @param {number} n
 * @return {number}
 */
var myPow = function(x, n) {

};
```

根据上面的已知函数，小伙伴们可以先尝试破解本题，确定了自己的答案后再看下面代码。

## 三 解题思路



* 递归（爆栈）

290 / 304 个通过测试用例：Line 20: RangeError: Maximum call stack size exceeded

```js
/**
 * @param {number} x
 * @param {number} n
 * @return {number}
 */
const myPow = (x, n) => {
  let result = 1; // 最终结果值
  let time = n; // 将递归次数给收集下
  let negativeFlag = false; // 判断是否为负数次方，是的话后面用 1 / result

  // 0 次方返回 1，负次方设置 flag
  if (n === 0) {
    return 1;
  } else if (n < 0) {
    time = -n;
    negativeFlag = true;
  }

  // 递归
  const recursion = (time) => {
    if (time < 1) {
      return 1;
    }
    result *= x;
    recursion(time - 1);
  };
  recursion(time);

  // 如果是负次方，返回 1 / result
  if (negativeFlag) {
    return 1 / result;
  }
  // 否则返回 result
  return result;
};

console.log(myPow(2, -2));
```

* 迭代（超时）

301 / 304 个通过测试用例：x = 2.00000；n = -2147483648

```js
/**
 * @param {number} x
 * @param {number} n
 * @return {number}
 */
const myPow = (x, n) => {
  let result = 1; // 最终结果值
  let time = n; // 将递归次数给收集下
  let negativeFlag = false; // 判断是否为负数次方，是的话后面用 1 / result

  // 0 次方返回 1，负次方设置 flag
  if (n === 0) {
    return 1;
  } else if (n < 0) {
    time = -n;
    negativeFlag = true;
  }

  // 迭代
  while (time) {
    result *= x;
    time--;
  }

  // 如果是负次方，返回 1 / result
  if (negativeFlag) {
    return 1 / result;
  }
  // 否则返回 result
  return result;
};

console.log(myPow(2, -2));
```

* 递归（优化）

```js
/**
 * @param {number} x
 * @param {number} n
 * @return {number}
 */
const myPow = (x, n) => {
  const isNegative = n < 0; // 是否是负指数

  // 递归
  const recursion = (n) => {
    if (n === 0) {
      return 1;
    } else if (n === 1) {
      return x;
    }
    const tempResult = recursion(Math.floor(n / 2));
    return n % 2 === 0 ? tempResult * tempResult : tempResult * tempResult * x;
  };

  const result = recursion(Math.abs(n));
  return isNegative ? 1 / result : result;
};
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

