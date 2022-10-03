191 - 位1的个数（number-of-1-bits）
===

> Create by **jsliang** on **2019-07-08 16:16:00**  
> Recently revised in **2019-09-18 11:42:00**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| [四 执行测试](#chapter-four) |
| [五 LeetCode Submit](#chapter-five) |
| [六 知识点](#chapter-six) |
| [七 解题思路](#chapter-seven) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：位运算
* **题目地址**：https://leetcode-cn.com/problems/number-of-1-bits/
* **题目内容**：

```
编写一个函数，输入是一个无符号整数，返回其二进制表达式中数字位数为 ‘1’ 的个数（也被称为汉明重量）。

示例 1：
输入：00000000000000000000000000001011
输出：3
解释：输入的二进制串 00000000000000000000000000001011 中，共有三位为 '1'。

示例 2：
输入：00000000000000000000000010000000
输出：1
解释：输入的二进制串 00000000000000000000000010000000 中，共有一位为 '1'。

示例 3：
输入：11111111111111111111111111111101
输出：31
解释：输入的二进制串 11111111111111111111111111111101 中，共有 31 位为 '1'。
 

提示：
请注意，在某些语言（如 Java）中，没有无符号整数类型。在这种情况下，输入和输出都将被指定为有符号整数类型，并且不应影响您的实现，因为无论整数是有符号的还是无符号的，其内部的二进制表示形式都是相同的。
在 Java 中，编译器使用二进制补码记法来表示有符号整数。因此，在上面的 示例 3 中，输入表示有符号整数 -3。
 

进阶:
如果多次调用这个函数，你将如何优化你的算法？
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var hammingWeight = function (n) {
  return ((n.toString(2)).match(/1/g) || []).length;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



1. `n`：`00000000000000000000000000001011`
2. `return`：`3`


## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
✔ Accepted
  ✔ 601/601 cases passed (96 ms)
  ✔ Your runtime beats 70.51 % of javascript submissions
  ✔ Your memory usage beats 20.53 % of javascript submissions (35.1 MB)
```

## <a name="chapter-six" id="chapter-six">六 知识点</a>



`toString()`：`toString()` 返回一个字符串，表示指定的数组及其元素。[`toString()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Array/toString.md)

## <a name="chapter-seven" id="chapter-seven">七 解题思路</a>



**精辟的一行代码，能解决问题就是王道**

在这次解答中，我们需要明确的是：

1. `n` 是一个整数，所以进来需要转换成 二进制 数：即 `n.toString(2)`
2. 有可能 `n` 是空的
3. 如果 `n` 有长度，则通过 `match(/1/g)` 来匹配其中的 1，它会返回一个数组。

```js
var hammingWeight = function (n) {
  return ((n.toString(2)).match(/1/g) || []).length;
};
```

这样，我们就拿到了最终的结果。

看到这么快就完了，小伙伴可能想：**jsliang** 又水了一篇，额O__O "…我能怎么办，我也很绝望啊：

1. 我不喜欢搞二进制，比较无聊。
2. 这种题在前端业务代码中的体现，真的非常非常非常少，实用性不大。

所以，小伙伴们可以自行探索，如果有不错的题解，可以私聊我或者直接留言。

> 参考代码 1

```js
var hammingWeight = function (n) {
  return n.toString(2).replace(/0/g, '').length;
};
```

> 参考代码 2

```js
var hammingWeight = function (n) {
  let c = 0;
  while (n != 0) {
    n = n & n - 1;
    c++;
  }
  return c;
};
```

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

