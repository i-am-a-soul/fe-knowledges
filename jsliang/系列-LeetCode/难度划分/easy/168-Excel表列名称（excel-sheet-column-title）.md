168 - Excel表列名称（excel-sheet-column-title）
===

> Create by **jsliang** on **2019-07-04 19:30:13**  
> Recently revised in **2019-09-18 10:43:31**

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
* **涉及知识**：数学
* **题目地址**：https://leetcode-cn.com/problems/excel-sheet-column-title/
* **题目内容**：

```
给定一个正整数，返回它在 Excel 表中相对应的列名称。

例如，

  1 -> A
  2 -> B
  3 -> C
  ...
  26 -> Z
  27 -> AA
  28 -> AB 
  ...

示例 1:
输入: 1
输出: "A"

示例 2:
输入: 28
输出: "AB"

示例 3:
输入: 701
输出: "ZY"
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var convertToTitle = function(n) {
  let res = '';
  while (n !== 0) {
    n--;
    res = String.fromCharCode(n % 26 + 65) + res;
    n = parseInt(n / 26);
  }
  return res;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



1. `703`
2. `return`：`AAA`

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
√ Accepted
  √ 18/18 cases passed (68 ms)
  √ Your runtime beats 92.89 % of javascript submissions
  √ Your memory usage beats 23.3 % of javascript submissions (33.7 MB)
```

## <a name="chapter-six" id="chapter-six">六 知识点</a>



`fromCharCode()`：静态 `String.fromCharCode()` 方法返回由指定的 UTF-16 代码单元序列创建的字符串。简单来说，就是接受一个 Unicode 值，然后返回一个字符串。例如 65 - A，66 - B。[`fromCharCode()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/String/fromCharCode.md)

## <a name="chapter-seven" id="chapter-seven">七 解题思路</a>



**首先**，小伙伴们一上手，可能会发现这就是一道找规律题。

那么，规律在哪呢？

* `[1-26]`：`[A-Z]`
* `[27-52]`：`[AA-AZ]`
* ……

就是说，假设我们求解 `27`，那么它结果是 `AA`。

**然后**，我们开始计算

1. 将 `27` 以满 `26` 进制的形式，就是说转了一圈又到新开始。`27 = 26 + 1`
2. 将 `(27 - 1) % 26`，得到的就是起始点 `0`，这里我们使用了 ASCII，`A` 在里面的对照就是 `65`、`B` 在里面的对照是 `66`……
3. 最后，`27` 转了一圈，应该换掉：`(27 - 1) / 26`，得到的就是它处在新一轮的第 `1` 个位置。
4. ……

**最终**，得知这个数为 `A` + `A`，即 `AA`

```js
var convertToTitle = function(n) {
  let res = '';
  while (n !== 0) {
    n--;
    res = String.fromCharCode(n % 26 + 65) + res;
    n = parseInt(n / 26);
  }
  return res;
};
```

## <a name="chapter-eight" id="chapter-eight">八 进一步探索</a>



由于 **jsliang** 想到的是 ASCII，然后看了下 LeetCode 的评论和题解，里面有自定义字典的，小伙伴们可以瞅瞅：

> 参考 1

```js
var convertToTitle = function(n) {
  let dict = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L',
             'M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z']
  let res = ''
  while (n !== 0) {
    n--
    let c = n % 26
    res = dict[c] + res
    n = parseInt(n / 26)
  }
  return res
};
```

> 参考 2

```js
var convertToTitle = function (n) {
  const dic = 'ZABCDEFGHIJKLMNOPQRSTUVWXYZ';
  let res = '';
  while (n / 26 > 1) {//如果还有进位
    let mod = n % 26;// 取得当前余数
    res = dic[mod] + res;// 将余数放入结果
    n = (n - (mod === 0 ? 26 : mod)) / 26;// 减去余数部分
  }
  res = dic[n] + res
  return res;
};
```

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

