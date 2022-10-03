1281 - 整数的各位积和之差（subtract-the-product-and-sum-of-digits-of-an-integer）
===

> Create by **jsliang** on **2020-02-01 17:19:30**  
> Recently revised in **2020-02-01 17:56:31**

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
* **涉及知识**：数学
* **题目地址**：https://leetcode-cn.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer/
* **题目内容**：

```
给你一个整数 n，
请你帮忙计算并返回该整数「各位数字之积」与「各位数字之和」的差。

示例 1：

输入：n = 234
输出：15 
解释：
各位数之积 = 2 * 3 * 4 = 24 
各位数之和 = 2 + 3 + 4 = 9 
结果 = 24 - 9 = 15

示例 2：

输入：n = 4421
输出：21
解释： 
各位数之积 = 4 * 4 * 2 * 1 = 32 
各位数之和 = 4 + 4 + 2 + 1 = 11 
结果 = 32 - 11 = 21

提示：

1 <= n <= 10^5

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} n
 * @return {number}
 */
var subtractProductAndSum = function(n) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 整数的各位积和之差
 * @param {number} n
 * @return {number}
 */
const subtractProductAndSum = (n) => {
  n = String(n);
  let product = Number(n[0]);
  let sum = Number(n[0]);
  for (let i = 1; i < n.length; i++) {
    product *= Number(n[i]);
    sum += Number(n[i]);
  }
  return product - sum;
};

console.log(subtractProductAndSum(234)); // 15
```

`node index.js` 返回：

```js
15
```

## 四 LeetCode Submit



```js
Accepted
* 123/123 cases passed (60 ms)
* Your runtime beats 88.13 % of javascript submissions
* Your memory usage beats 62.2 % of javascript submissions (33.8 MB)
```

## 五 解题思路



这道题，感觉没点含量啊，连【简单】都不能算了，只能说是【入门】了：

> 暴力破解

```js
const subtractProductAndSum = (n) => {
  n = String(n);
  let product = Number(n[0]);
  let sum = Number(n[0]);
  for (let i = 1; i < n.length; i++) {
    product *= Number(n[i]);
    sum += Number(n[i]);
  }
  return product - sum;
};
```

Submit 提交：

```js
Accepted
* 123/123 cases passed (60 ms)
* Your runtime beats 88.13 % of javascript submissions
* Your memory usage beats 62.2 % of javascript submissions (33.8 MB)
```

好吧，不知道说啥好了，这道题 over 了。

如果小伙伴有更好的思路想法……enm...真会有么，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

