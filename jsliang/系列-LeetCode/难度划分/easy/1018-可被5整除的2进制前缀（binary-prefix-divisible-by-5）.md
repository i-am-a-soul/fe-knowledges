1018 - 可被5整除的2进制前缀（binary-prefix-divisible-by-5）
===

> Create by **jsliang** on **2020-01-29 20:54:27**  
> Recently revised in **2020-01-29 22:01:03**

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
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/binary-prefix-divisible-by-5/
* **题目内容**：

```
给定由若干 0 和 1 组成的数组 A。
我们定义 N_i：
从 A[0] 到 A[i] 的第 i 个子数组，
被解释为一个二进制数（从最高有效位到最低有效位）。

返回布尔值列表 answer，
只有当 N_i 可以被 5 整除时，
答案 answer[i] 为 true，否则为 false。

示例 1：

输入：[0,1,1]
输出：[true,false,false]
解释：
输入数字为 0, 01, 011；
也就是十进制中的 0, 1, 3 。
只有第一个数可以被 5 整除，
因此 answer[0] 为真。

示例 2：

输入：[1,1,1]
输出：[false,false,false]

示例 3：

输入：[0,1,1,1,1,1]
输出：[true,false,false,false,true,false]

示例 4：

输入：[1,1,1,0,1]
输出：[false,false,false,false,false]

提示：

1 <= A.length <= 30000
A[i] 为 0 或 1

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/binary-prefix-divisible-by-5
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} A
 * @return {boolean[]}
 */
var prefixesDivBy5 = function(A) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 可被5整除的二进制前缀
 * @param {number[]} A
 * @return {boolean[]}
 */
const prefixesDivBy5 = (A) => {
  let total = 0;
  const answer = [];
  for (let i = 0; i < A.length; i++) {
    total = (total * 2 + A[i]) % 10;
    answer.push(total === 0 || total === 5);
  }
  return answer;
};

console.log(prefixesDivBy5([0, 1, 1])); // [true, false, false]
```

`node index.js` 返回：

```js
[ true, false, false ]
```

## 四 LeetCode Submit



```js
Accepted
* 24/24 cases passed (76 ms)
* Your runtime beats 95.95 % of javascript submissions
* Your memory usage beats 89.83 % of javascript submissions (38 MB)
```

## 五 解题思路



“好像没那么复杂”：

> 暴力破解【超时】

```js
const prefixesDivBy5 = (A) => {
  let binary = '';
  const result = [];
  for (let i = 0; i < A.length; i++) {
    binary += A[i];
    if (parseInt(binary, 2) % 5 === 0) {
      result.push(true);
    } else {
      result.push(false);
    }
  }
  return result;
};
```

通过字符串累计每个字节，然后判断是否能 % 5 即可。

然后就出问题了：

```
Wrong Answer
* 9/24 cases passed (N/A)

Testcase
* [1,0,1,0,0,0,0,0,0,0,0, ...省略..., 0,0,1,1,0,0,1,1,1]

Answer
* [false,false,true, ...省略..., ,false,false]

Expected Answer
* [false,false,true,true, ...省略...,false,false]
```

初步判断应该是这个二进制过长，然后转换过程出了问题，导致不能正常转换~

这有点类似于大数（bigNumber）的加减会有问题一样。

无解，十进制转二进制我懂，二进制转十进制不太清楚啊！

> 这个弊端应该是所有编程语言都会出现，即涉及到大数运算时，精度缺失问题

## 六 进一步思考



事实证明，授之于鱼不如授之以渔。

> 【题解区】

```js
const prefixesDivBy5 = (A) => {
  let total = 0;
  const answer = [];
  for (let i = 0; i < A.length; i++) {
    total = (total * 2 + A[i]) % 10;
    answer.push(total === 0 || total === 5);
  }
  return answer;
};
```

我们并不需要进行完全转换，只需要判断这个数的末尾是否为 0 或者 5 即可。

> 能被 5 整除的数，末尾为 0 或者 5。

所以，二进制转换十进制如何操作？

**jsliang** 开了篇文章讲解：

1. 正整数转二进制
2. 负整数转二进制
3. 小数转二进制
4. ……

地址如下：

* https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%85%B6%E4%BB%96/%E5%8D%81%E8%BF%9B%E5%88%B6%E5%92%8C%E4%BA%8C%E8%BF%9B%E5%88%B6%E4%BA%92%E7%9B%B8%E8%BD%AC%E6%8D%A2.md

Submit 提交：

```js
Accepted
* 24/24 cases passed (76 ms)
* Your runtime beats 95.95 % of javascript submissions
* Your memory usage beats 89.83 % of javascript submissions (38 MB)
```

这样，我们就完成这道题的讲解，如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

