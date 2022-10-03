1137 - 第N个泰波那契数（n-th-tribonacci-number）
===

> Create by **jsliang** on **2020-01-31 14:29:12**  
> Recently revised in **2020-01-31 15:01:03**

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题及测试](#chapter-three) |
| [四 LeetCode Submit](#chapter-four) |
| [五 解题思路](#chapter-five) |
| [六 进一步思考](#chapter-six) |

## 二 前言



* **难度**：简单
* **涉及知识**：递归
* **题目地址**：https://leetcode-cn.com/problems/n-th-tribonacci-number/
* **题目内容**：

```
泰波那契序列 Tn 定义如下： 

T0 = 0, T1 = 1, T2 = 1, 
且在 n >= 0 的条件下 Tn+3 = Tn + Tn+1 + Tn+2

给你整数 n，请返回第 n 个泰波那契数 Tn 的值。

示例 1：

输入：n = 4
输出：4
解释：
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4

示例 2：

输入：n = 25
输出：1389537

提示：

0 <= n <= 37
答案保证是一个 32 位整数，即 answer <= 2^31 - 1。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/n-th-tribonacci-number
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
var tribonacci = function(n) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 第N个泰波那契数
 * @param {number} n
 * @return {number}
 */
const tribonacci = (n) => {
  // 1. 设置 list 记录表
  const list = [];
  // 2. 设置 ergidic 进行递归
  const ergodic = (n) => {
    // 3. 如果有这个内容，直接返回
    if (list[n]) {
      return list[n];
    }
    // 4. 如果没有，就进行正常操作
    if (n === 0) {
      return 0;
    } else if (n === 1) {
      return 1;
    } else if (n === 2) {
      return 1;
    } else {
      const num = ergodic(n - 3) + ergodic(n - 2) + ergodic(n  - 1);
      // 4.1 特别注意，进行 list 添加
      list[n] = num;
      return num;
    }
  }
  // 5. 返回结果
  return ergodic(n);
};

console.log(tribonacci(37)); // 2082876103
```

`node index.js` 返回：

```js
2082876103
```

## 四 LeetCode Submit



```js
Accepted
* 39/39 cases passed (76 ms)
* Your runtime beats 10.07 % of javascript submissions
* Your memory usage beats 88.94 % of javascript submissions (33.6 MB)
```

## 五 解题思路



是的，你没看错，就是【泰】波波那契数，一开始我还以为是斐波那契数列，想了老久这应该是自定义数列？

> 百度没有搜索到这种数列

那么，开始解题：

> 暴力破解【超时】

```js
const tribonacci = (n) => {
  if (n === 0) {
    return 0;
  } else if (n === 1) {
    return 1
  } else if (n === 2) {
    return 1
  } else {
    return tribonacci(n - 1) + tribonacci(n - 2) + tribonacci(n - 3);
  }
};
```

惯用思路就是递归啦，然而这有点不好的就是它会超时。

Submit 提交：

```js
Time Limit Exceeded
* 36/39 cases passed (N/A)

Testcase
* 35
```

想当年搞斐波那契数列，见过一种粗暴方法：

> 超暴力破解

```js
const tribonacci = (n) => [0, 1, 1, 2, 4, 7, 13, 24, 44, 81, 149, 274, 504, 927, 1705, 3136, 5768, 10609, 19513, 35890, 66012, 121415, 223317, 410744, 755476, 1389537, 2555757, 4700770, 8646064, 15902591, 29249425, 53798080, 98950096, 181997601, 334745777, 615693474, 1132436852, 2082876103][n];
```

Submit 提交：

```js
Accepted
* 39/39 cases passed (60 ms)
* Your runtime beats 75.69 % of javascript submissions
* Your memory usage beats 38.46 % of javascript submissions (33.8 MB)
```

好了，这种测试用例编程仅能玩玩，咱们还是考虑下优化下递归~

> 递归 + 哈希表

```js
const tribonacci = (n) => {
  // 1. 设置 list 记录表
  const list = [];
  // 2. 设置 ergidic 进行递归
  const ergodic = (n) => {
    // 3. 如果有这个内容，直接返回
    if (list[n]) {
      return list[n];
    }
    // 4. 如果没有，就进行正常操作
    if (n === 0) {
      return 0;
    } else if (n === 1) {
      return 1;
    } else if (n === 2) {
      return 1;
    } else {
      const num = ergodic(n - 3) + ergodic(n - 2) + ergodic(n  - 1);
      // 4.1 特别注意，进行 list 添加
      list[n] = num;
      return num;
    }
  }
  // 5. 返回结果
  return ergodic(n);
};
```

如上，我们将一开始超时的递归方法，进行优化，添加个 `list` 记录列表即可。

Submit 提交：

```js
Accepted
* 39/39 cases passed (76 ms)
* Your runtime beats 10.07 % of javascript submissions
* Your memory usage beats 88.94 % of javascript submissions (33.6 MB)
```

## 六 进一步思考



那么接下来去瞅瞅大佬操作了~

> 【题解区】自底向上

```js
const tribonacci = (n) => {
  if (n === 0) {
    return 0;
  } else if (n === 1) {
    return 1;
  } else if (n === 2) {
    return 1;
  }
  let a = 0, b = 1, c = 1;
  for (let i = 3; i <= n; i++) {
    const temp = a + b + c;
    a = b;
    b = c;
    c = temp;
  }
  return c;
};
```

Submit 提交：

```js
Accepted
* 39/39 cases passed (60 ms)
* Your runtime beats 75.69 % of javascript submissions
* Your memory usage beats 94.23 % of javascript submissions (33.6 MB)
```

非常 nice 的想法啦，通过一次循环逐个添加即可。

当然，如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

