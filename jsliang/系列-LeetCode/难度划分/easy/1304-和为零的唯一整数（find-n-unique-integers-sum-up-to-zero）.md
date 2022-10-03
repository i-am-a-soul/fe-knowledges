1304 - 和为零的唯一整数（find-n-unique-integers-sum-up-to-zero）
===

> Create by **jsliang** on **2020-02-01 19:45:26**  
> Recently revised in **2020-02-01 19:56:53**

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
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/find-n-unique-integers-sum-up-to-zero/
* **题目内容**：

```
给你一个整数 n，
请你返回 任意 一个由 n 个 各不相同 的整数组成的数组，
并且这 n 个数相加和为 0 。

示例 1：

输入：n = 5
输出：[-7,-1,1,3,4]
解释：这些数组也是正确的 [-5,-1,1,2,3]，[-3,-1,2,-2,4]。

示例 2：

输入：n = 3
输出：[-1,0,1]

示例 3：

输入：n = 1
输出：[0]

提示：

1 <= n <= 1000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-n-unique-integers-sum-up-to-zero
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} n
 * @return {number[]}
 */
var sumZero = function(n) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 和为零的n个唯一整数
 * @param {number} n
 * @return {number[]}
 */
const sumZero = (n) => {
  let number = n,
      flag = false;
  const result = [];
  for (let i = 0; i < n; i++) {
    if (flag) {
      result.push(-number);
      number--;
      flag = false;
    } else {
      result.push(number);
      flag = true;
    }
  }
  if (result.length % 2 === 1) {
    result[result.length - 1] = 0;
  }
  return result;
};

console.log(sumZero(5)); // [ 5, -5, 4, -4, 0 ]
```

`node index.js` 返回：

```js
[ 5, -5, 4, -4, 0 ]
```

## 四 LeetCode Submit



```js
Accepted
* 42/42 cases passed (64 ms)
* Your runtime beats 87.12 % of javascript submissions
* Your memory usage beats 83.1 % of javascript submissions (34.9 MB)
```

## 五 解题思路



这道题给了 **jsliang** 最大程度的自由，所以可以随心所欲，任性发挥：

> 暴力破解

```js
const sumZero = (n) => {
  // 1. 定义变量
  let number = n,
      flag = false;
  
  // 2. 定义结果值
  const result = [];
  for (let i = 0; i < n; i++) {
    // 2.1 判断是输入正数还是负数
    if (flag) {
      result.push(-number);
      number--;
      flag = false;
    } else {
      result.push(number);
      flag = true;
    }
  }

  // 3. 判断是否为奇数长度位
  if (result.length % 2 === 1) {
    result[result.length - 1] = 0;
  }

  // 4. 输出结果
  return result;
};
```

是的，正如上面所写，如果 `n` 为 5，那么输出：

* [5, -5, 4, -4, 0]

如果 `n` 为 4，那么输出：

* [4, -4, 3, -3]

Submit 提交：

```js
Accepted
* 42/42 cases passed (64 ms)
* Your runtime beats 87.12 % of javascript submissions
* Your memory usage beats 83.1 % of javascript submissions (34.9 MB)
```

那么本题题解就到这里。

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

