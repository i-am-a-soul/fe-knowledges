1009 - 十进制整数的反码（complement-of-base-10-integer）
===

> Create by **jsliang** on **2020-01-29 17:35:05**  
> Recently revised in **2020-01-29 18:04:39**

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
* **题目地址**：https://leetcode-cn.com/problems/complement-of-base-10-integer/
* **题目内容**：

```
每个非负整数 N 都有其二进制表示。

例如，
5 可以被表示为二进制 "101"，
11 可以用二进制 "1011" 表示，
依此类推。

注意，除 N = 0 外，任何二进制表示中都不含前导零。

二进制的反码表示是将每个 1 改为 0 且每个 0 变为 1。

例如，二进制数 "101" 的二进制反码为 "010"。

给定十进制数 N，返回其二进制表示的反码所对应的十进制整数。

示例 1：

输入：5
输出：2
解释：5 的二进制表示为 "101"，其二进制反码为 "010"，也就是十进制中的 2 。

示例 2：

输入：7
输出：0
解释：7 的二进制表示为 "111"，其二进制反码为 "000"，也就是十进制中的 0 。

示例 3：

输入：10
输出：5
解释：10 的二进制表示为 "1010"，其二进制反码为 "0101"，也就是十进制中的 5 。

提示：

0 <= N < 10^9

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/complement-of-base-10-integer
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} N
 * @return {number}
 */
var bitwiseComplement = function(N) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 十进制整数的反码
 * @param {number} N
 * @return {number}
 */
const bitwiseComplement = (N) => {
  let binary = '';
  while (N > 0) {
    if (N % 2 === 0) {
      binary = '1' + binary;
    } else {
      binary = '0' + binary;
    }
    N = Math.floor(N / 2);
  }
  return parseInt(binary || '1', 2);
};

console.log(bitwiseComplement(7)); // 0
```

`node index.js` 返回：

```js
0
```

## 四 LeetCode Submit



```js
Accepted
* 128/128 cases passed (60 ms)
* Your runtime beats 84.91 % of javascript submissions
* Your memory usage beats 69.88 % of javascript submissions (33.7 MB)
```

## 五 解题思路



看完题目就有思路了，主要是十进制转二进制的基础操作，这里从浅入深，逐步完善讲解：

> 十进制转二进制

```js
/**
 * @name 十进制转二进制
 * @param {number} num 需要转换的数字
 * @return {string}
 */
const decimalToBinary = (num) => {
  let result = '';
  while (num > 0) {
    result = (num % 2) + result;
    num = Math.floor(num / 2);
  }
  return result;
};
console.log(decimalToBinary(5));
```

打印结果为 `'101'`，这样我们就有了十进制转二进制的方法，这道题的答案呼之欲出：

> 暴力破解

```js
/**
 * @name 十进制转二进制
 * @param {number} num 需要转换的数字
 * @return {string}
 */
const decimalToBinary = (num) => {
  if (num === 0) {
    return '0';
  }
  let result = '';
  while (num > 0) {
    result = (num % 2) + result;
    num = Math.floor(num / 2);
  }
  return result;
};

/**
 * @name 十进制整数的反码
 * @param {number} N
 * @return {number}
 */
const bitwiseComplement = (N) => {
  const binary = decimalToBinary(N);
  let newBinary = '';
  for (let i = 0; i < binary.length; i++) {
    if (binary[i] === '1') {
      newBinary += '0';
    } else {
      newBinary += '1';
    }
  }
  return parseInt(newBinary, 2);
};

console.log(bitwiseComplement(7)); // 0
```

Submit 提交：

```js
Accepted
* 128/128 cases passed (60 ms)
* Your runtime beats 84.91 % of javascript submissions
* Your memory usage beats 54.22 % of javascript submissions (33.7 MB)
```

但是，看到 `parseInt(newBinary, 2)`，小伙伴应该瞬间明悟：

* 卧槽有原生方法将二进制转十进制，那么应该也有方法将十进制转二进制的吧！

是的：

> 【优化一】利用原生 API

```js
const bitwiseComplement = (N) => {
  const binary = N.toString(2);
  let newBinary = '';
  for (let i = 0; i < binary.length; i++) {
    if (binary[i] === '1') {
      newBinary += '0';
    } else {
      newBinary += '1';
    }
  }
  return parseInt(newBinary, 2);
};
```

Submit 提交：

```js
Accepted
* 128/128 cases passed (72 ms)
* Your runtime beats 32.08 % of javascript submissions
* Your memory usage beats 51.81 % of javascript submissions (33.8 MB)
```

并不是我乱写，但是我自己写的方法是 `runtime beats 84.91 %`，原生是 `runtime beats 32.08 %`。

因为原生考虑的不仅仅是这么点内容，你懂的。

> 【优化二】简化暴力破解

```js
const bitwiseComplement = (N) => {
  let binary = '';
  while (N > 0) {
    if (N % 2 === 0) {
      binary = '1' + binary;
    } else {
      binary = '0' + binary;
    }
    N = Math.floor(N / 2);
  }
  return parseInt(binary || '1', 2);
};
```

Submit 提交：

```js
Accepted
* 128/128 cases passed (60 ms)
* Your runtime beats 84.91 % of javascript submissions
* Your memory usage beats 54.22 % of javascript submissions (33.7 MB)
```

这里我们直接将转换的方法搬过来，然后需要直接转换 1 和 0 即可。

最后需要注意的是，0 会被转换成 NaN，所以我们直接给个 `'1'` 就好~

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

