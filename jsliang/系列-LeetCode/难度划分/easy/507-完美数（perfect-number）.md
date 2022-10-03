507 - 完美数（perfect-number）
===

> Create by **jsliang** on **2019-11-3 11:48:39**  
> Recently revised in **2019-11-3 12:23:01**

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
* **涉及知识**：数学
* **题目地址**：https://leetcode-cn.com/problems/perfect-number/
* **题目内容**：

```
对于一个 正整数，如果它和除了它自身以外的所有正因子之和相等，我们称它为“完美数”。

给定一个 整数 n， 如果他是完美数，返回 True，否则返回 False

示例：
输入: 28
输出: True
解释: 28 = 1 + 2 + 4 + 7 + 14
 

提示：
输入的数字 n 不会超过 100,000,000. (1e8)
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} num
 * @return {boolean}
 */
var checkPerfectNumber = function(num) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 完美数
 * @param {number} num
 * @return {boolean}
 */
const checkPerfectNumber = (num) => {
  const positiveFactors = [1];
  const hash = new Map();
  for (let i = 2; i < num / 2; i++) {
    if (Number.isInteger(num / i) && !hash.get(i)) {
      positiveFactors.push(i);
      positiveFactors.push(num / i);
      hash.set(num / i, i);
    }
  }
  const result = positiveFactors.reduce((prev, curr) => {
    return prev + curr;
  });
  return num !== 1 && result === num;
};

const num = 28;
console.log(checkPerfectNumber(num));
```

`node index.js` 返回：

```js
true
```

## 四 LeetCode Submit



```js
Accepted
* 156/156 cases passed (2128 ms)
* Your runtime beats 29.79 % of javascript submissions
* Your memory usage beats 14.29 % of javascript submissions (35.2 MB)
```

## 五 解题思路



看到题目，思考内容：

1. 如果将传入的数字 `n` 进行遍历，找出所有的因素，那么会不会爆时，毕竟 `1e8` 的长度还是挺大的。

所以，我们尝试暴力破解先：

```js
/**
 * @name 完美数
 * @param {number} num
 * @return {boolean}
 */
const checkPerfectNumber = (num) => {
  const positiveFactors = [1];
  const hash = new Map();
  for (let i = 2; i < num / 2; i++) {
    if (Number.isInteger(num / i) && !hash.get(i)) {
      positiveFactors.push(i);
      positiveFactors.push(num / i);
      hash.set(num / i, i);
    }
  }
  const result = positiveFactors.reduce((prev, curr) => {
    return prev + curr;
  });
  return num !== 1 && result === num;
};
```

Submit 提交：

```js
Accepted
* 156/156 cases passed (2128 ms)
* Your runtime beats 29.79 % of javascript submissions
* Your memory usage beats 14.29 % of javascript submissions (35.2 MB)
```

结果是可行的，虽然 **jsliang** 个人感觉还是不太满意，但是可以先讲讲思路：

1. 先在 `return` 处排除 1 的情况，因为它是个个例，需要单独分开。
2. 每个数必定存在正因数 1，所以将 1 放在初始化正因数 `positiveFactors` 的数组中。
3. 遍历 `num`，但是我们仅遍历一半，因为我们从 2 开始计算（拆半）。
4. 如果 `num / i` 是一个正整数，那么我们就存储两个正因数 `i` 和 `num / i`，同时，我们将 `num / i` 存储到哈希表上，防止重复统计。
5. 累加所有正因数之和，如果和原有的 `num` 相等，那么它就是正因数！

如上，我们就破解了这道题。

## 六 进一步思考



为了更好的学习提升，咱们再逛逛【题解】和【评论】区，看看有什么 idea 是我们没想到，但是非常好用的：

> index.js

```js
const checkPerfectNumber = (num) => {
  return num === 6 || num === 28 || num === 496 || num === 8128 || num === 33550336;
};
```

Submit 试试：

```js
Accepted
* 156/156 cases passed (76 ms)
* Your runtime beats 71.63 % of javascript submissions
* Your memory usage beats 100 % of javascript submissions (33.6 MB)
```

这种方法叫做：我知道你的答案，所以我来个面向测试用例开发。/ 手动滑稽

> 这种方法来自【题解】的灵感：https://leetcode-cn.com/problems/perfect-number/solution/507-wan-mei-shu-by-yukarun/ 

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

