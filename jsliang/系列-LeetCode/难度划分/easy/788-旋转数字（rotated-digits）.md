788 - 旋转数字（rotated-digits）
===

> Create by **jsliang** on **2020-01-05 08:40:01**  
> Recently revised in **2020-01-05 09:27:32**

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
* **涉及知识**：字符串
* **题目地址**：https://leetcode-cn.com/problems/rotated-digits/
* **题目内容**：

```
我们称一个数 X 为好数, 
如果它的每位数字逐个地被旋转 180 度后，
我们仍可以得到一个有效的，
且和 X 不同的数。
要求每位数字都要被旋转。

如果一个数的每位数字被旋转以后仍然还是一个数字，
则这个数是有效的。
0, 1, 和 8 被旋转后仍然是它们自己；
2 和 5 可以互相旋转成对方；
6 和 9 同理，
除了这些以外其他的数字旋转以后都不再是有效的数字。

现在我们有一个正整数 N, 
计算从 1 到 N 中有多少个数 X 是好数？

示例:
输入: 10
输出: 4
解释: 
在[1, 10]中有四个好数： 2, 5, 6, 9。
注意 1 和 10 不是好数, 因为他们在旋转之后不变。

注意:

N 的取值范围是 [1, 10000]。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} N
 * @return {number}
 */
var rotatedDigits = function(N) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 旋转数字
 * @param {number} N
 * @return {number}
 */
const rotatedDigits = (N) => {
  let result = 0;
  for (let i = 1; i <= N; i++) {
    const arrNum = String(i);
    if (arrNum.includes('3') || arrNum.includes('4') || arrNum.includes('7')) {
      continue;
    }
    if (arrNum.includes('2') || arrNum.includes('5') || arrNum.includes('6') || arrNum.includes('9')) {
      result++;
    }
  }
  return result;
};

console.log(rotatedDigits(857)); // 247
```

`node index.js` 返回：

```js
247
```

## 四 LeetCode Submit



```js
Accepted
* 50/50 cases passed (76 ms)
* Your runtime beats 69.39 % of javascript submissions
* Your memory usage beats 68.42 % of javascript submissions (35.4 MB)
```

## 五 解题思路



**首先**，理解定义：

* 好数

1. 每个数字旋转 180°；
2. 得到的数字是有效的；
3. 和原数字不同。

> 暴力破解

```js
const rotatedDigits = (N) => {
  const result = [];
  for (let i = 1; i <= N; i++) {
    const arrNum = i.toString().split('');
    let flag = false;
    for (let j = 0; j < arrNum.length; j++) {
      switch (arrNum[j]) {
        case '2':
          arrNum[j] = '5'; break;
        case '5':
          arrNum[j] = '2'; break;
        case '6':
          arrNum[j] = '9'; break;
        case '9':
          arrNum[j] = '6'; break;
        case '3': case '4': case '7':
          flag = true; break;
        default: break;
      }
      if (flag) {
        break;
      }
    }
    if (Number(arrNum.join('')) !== i && !flag) {
      result.push(i);
    }
  }
  return result.length;
};
```

思路如下：

1. 遍历 [1, N] 区间的所有数字；
2. 将该数字转换成数组（方便替换数字）；
3. 判断 2、5、9、6，则进行翻转；
4. 判断 3、4、7，则进行不信任；
5. 判断翻转后的数组通过 `Number(arr.join(''))` 后的数字和原数字是否相同，并且 `flag` 这个标志不能为 `true`，则这个数字可以旋转。

Submit 提交如下：

```js
Accepted
* 50/50 cases passed (120 ms)
* Your runtime beats 11.22 % of javascript submissions
* Your memory usage beats 26.32 % of javascript submissions (37.7 MB)
```

**然后**，再仔细找找规律：

> 规律破解

```js
const rotatedDigits = (N) => {
  let result = 0;
  for (let i = 1; i <= N; i++) {
    const arrNum = String(i);
    if (arrNum.includes('3') || arrNum.includes('4') || arrNum.includes('7')) {
      continue;
    }
    if (arrNum.includes('2') || arrNum.includes('5') || arrNum.includes('6') || arrNum.includes('9')) {
      result++;
    }
  }
  return result;
};
```

众所周知，`String` 和 `Array` 都有一个 `includes` 方法，通过分类判断：

* 如果这个数字包含 3、4、7，那么它不能旋转；
* 如果这个数字包含 2、5、6、9，那么它可以旋转。

比暴力更便捷：

```js
Accepted
* 50/50 cases passed (76 ms)
* Your runtime beats 69.39 % of javascript submissions
* Your memory usage beats 68.42 % of javascript submissions (35.4 MB)
```

**最后**，如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

