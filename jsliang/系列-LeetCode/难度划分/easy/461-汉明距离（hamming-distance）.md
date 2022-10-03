461 - 汉明距离（hamming-distance）
===

> Create by **jsliang** on **2019-10-23 09:47:04**  
> Recently revised in **2019-10-23 11:44:45**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题即测试](#chapter-three) |
| [四 LeetCode Submit](#chapter-four) |
| [五 解题思路](#chapter-five) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：位运算
* **题目地址**：https://leetcode-cn.com/problems/hamming-distance/
* **题目内容**：

```
两个整数之间的汉明距离指的是这两个数字对应二进制位不同的位置的数目。

给出两个整数 x 和 y，计算它们之间的汉明距离。

注意：
0 ≤ x, y < 231.

示例:

输入: x = 1, y = 4

输出: 2

解释:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑

上面的箭头指出了对应二进制位不同的位置。
```

## <a name="chapter-three" id="chapter-three">三 解题及测试</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

> index.js

```js
/**
 * @param {number} x
 * @param {number} y
 * @return {number}
 */
const hammingDistance = (x, y) => {
  let cnt = 0;
  while (x != 0 || y != 0) {
    if ((x & 1) != (y & 1)) {
      cnt++;
    }
    x >>= 1;
    y >>= 1;
  }
  return cnt;
};

console.log(hammingDistance(1, 4));
```

`node index.js` 返回：

```js
2
```

## <a name="chapter-four" id="chapter-four">四 LeetCode Submit</a>



```js
149/149 cases passed (64 ms)
Your runtime beats 92.11 % of javascript submissions
Your memory usage beats 53.01 % of javascript submissions (33.7 MB)
```

## <a name="chapter-five" id="chapter-five">五 解题思路</a>



无法解释，因为 **jsliang** 也不太了解位运算！/(ㄒoㄒ)/~~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

