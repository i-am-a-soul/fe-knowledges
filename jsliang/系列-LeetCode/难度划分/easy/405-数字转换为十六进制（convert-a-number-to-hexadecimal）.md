405 - 数字转换为十六进制（convert-a-number-to-hexadecimal）
===

> Create by **jsliang** on **2019-07-25 10:45:31**  
> Recently revised in **2019-09-18 14:01:34**

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
* **题目地址**：https://leetcode-cn.com/problems/convert-a-number-to-hexadecimal/
* **题目内容**：

```
给定一个整数，编写一个算法将这个数转换为十六进制数。
对于负整数，我们通常使用 补码运算 方法。

注意:

1. 十六进制中所有字母(a-f)都必须是小写。
2. 十六进制字符串中不能包含多余的前导零。
如果要转化的数为 0，那么以单个字符'0'来表示；
对于其他情况，十六进制字符串中的第一个字符将不会是0字符。 
3. 给定的数确保在32位有符号整数范围内。
4. 不能使用任何由库提供的将数字直接转换或格式化为十六进制的方法。

示例 1：
输入:
26
输出:
"1a"

示例 2：
输入:
-1
输出:
"ffffffff"
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var toHex = function (num) {
  if (!num) {
    return '0';
  }
  num = num > -1 ? num : num + Math.pow(2, 32);
  let res = '',
    Hex = '0123456789abcdef';
  while (num) {
    res = Hex[num % 16] + res;
    num = num / 16 | 0;
  }
  return res;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



1. `num`：`26`
2. `return`：

```js
1a
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
✔ Accepted
  ✔ 100/100 cases passed (108 ms)
  ✔ Your runtime beats 8.7 % of javascript submissions
  ✔ Your memory usage beats 6.06 % of javascript submissions (34.2 MB)
```

## <a name="chapter-six" id="chapter-six">六 知识点</a>



1. `Math`：JS 中的内置对象，具有数学常数和函数的属性和方法。[`Math` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Math/README.md)

## <a name="chapter-seven" id="chapter-seven">七 解题思路</a>



**首先**，这道位运算，真的真的真的不想做。

**然后**，强忍住一脸懵逼，找到了一道题解，再细细解析：

1. 如果这个数是负数，需要补码，补码即加上 2 的 32 次幂。
2. 将这个数 `%16`，得到的是当前位的十六进制，将其添加到 `res` 前面。
3. 将这个数 `/16` 来进行循环遍历，直至这个数小于或者等于 0 为止。

**最后**，返回最终求解。

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

