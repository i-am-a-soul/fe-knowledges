371 - 两整数之和（sum-of-two-integers）
===

> Create by **jsliang** on **2019-07-23 17:01:33**  
> Recently revised in **2019-07-23 17:14:46**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| [四 执行测试](#chapter-four) |
| [五 LeetCode Submit](#chapter-five) |
| [六 解题思路](#chapter-six) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：位运算
* **题目地址**：https://leetcode-cn.com/problems/sum-of-two-integers/
* **题目内容**：

```
不使用运算符 + 和 - ​​​​​​​，计算两整数 ​​​​​​​a 、b ​​​​​​​之和。

示例 1:
输入: a = 1, b = 2
输出: 3

示例 2:
输入: a = -2, b = 3
输出: 1
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var getSum = function (a, b) {
  var sum = a ^ b;
  var carry = (a & b) << 1;
  while (carry) {
    var temp = sum;
    sum ^= carry;
    carry = (temp & carry) << 1;
  }
  return sum;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



1. `a`：`1`
2. `b`：`2`
3. `return`：

```js
3
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
✔ Accepted
  ✔ 13/13 cases passed (92 ms)
  ✔ Your runtime beats 27.45 % of javascript submissions
  ✔ Your memory usage beats 98.92 % of javascript submissions (33.3 MB)
```

## <a name="chapter-six" id="chapter-six">六 解题思路</a>



**首先**，恕我愚钝，上来就是破坏题意：

```js
var getSum = function(a, b) {
  return a + b;
};
```

得到 Submit：

```js
✔ Accepted
  ✔ 13/13 cases passed (104 ms)
  ✔ Your runtime beats 20.91 % of javascript submissions
  ✔ Your memory usage beats 98.92 % of javascript submissions (33.3 MB)
```

居然还成功了，虽然在面试中，可能第一个会被淘汰掉的吧……

因为……我不会位运算啊！！！

**然后**，还是看看大佬怎么做的吧：

```js
var getSum = function (a, b) {
  /* 按位与：只有两个操作数中相应位为 1 结果才为 1，其余情况结果为 0。
   * 按位异或：只有两个操作数同时为 1 或为 0 结果为 0，其余情况结果为 1。
   * + 运算符：两操作数同时为 1 结果为 0 并进位 1，其余为 0。
   */
  var sum = a ^ b;
  var carry = (a & b) << 1;
  while (carry) {
    var temp = sum;
    sum ^= carry;
    carry = (temp & carry) << 1;
  }
  return sum;
};
```

Submit 后：

```js
✔ Accepted
  ✔ 13/13 cases passed (92 ms)
  ✔ Your runtime beats 27.45 % of javascript submissions
  ✔ Your memory usage beats 98.92 % of javascript submissions (33.3 MB)
```

**最后**，咱就不做过多评论啦，毕竟 **位运算** 这个点，**jsliang** 还是太薄弱了（毕竟工作中几乎不会用到啊）。

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

