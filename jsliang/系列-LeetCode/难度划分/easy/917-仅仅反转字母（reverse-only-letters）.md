917 - 仅仅反转字母（reverse-only-letters）
===

> Create by **jsliang** on **2020-01-23 20:28:12**  
> Recently revised in **2020-01-23 21:20:21**

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
* **涉及知识**：字符串
* **题目地址**：https://leetcode-cn.com/problems/reverse-only-letters/
* **题目内容**：

```
给定一个字符串 S，
返回 “反转后的” 字符串，
其中不是字母的字符都保留在原地，
而所有字母的位置发生反转。

示例 1：

输入："ab-cd"
输出："dc-ba"

示例 2：

输入："a-bC-dEf-ghIj"
输出："j-Ih-gfE-dCba"

示例 3：

输入："Test1ng-Leet=code-Q!"
输出："Qedo1ct-eeLg=ntse-T!"

提示：

S.length <= 100
33 <= S[i].ASCIIcode <= 122 
S 中不包含 \ or "

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reverse-only-letters
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var islandPerimeter = function(grid) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 仅仅反转字母
 * @param {string} S
 * @return {string}
 */
const reverseOnlyLetters = (S) => {
  const newS = S.split('');
  const harf = Math.floor(newS.length / 2);
  for (let i = 0, j = newS.length - 1; i < harf, j > i; i++, j--) {
    const tempSI = newS[i].toUpperCase().charCodeAt(),
          tempSJ = newS[j].toUpperCase().charCodeAt();
    // 两边为字母，正常交换
    if (
      (tempSI >= 65 && tempSI <= 90)
      && (tempSJ >= 65 && tempSJ <= 90)
    ) {
      const temp = newS[i];
      newS[i] = newS[j];
      newS[j] = temp;
    }
    // 左侧值异常，右侧值不动
    if (
      (tempSI < 65 || tempSI > 90)
      && (tempSJ >= 65 && tempSJ <= 90)
    ) {
      j++;
    }
    // 右侧值异常，左侧值不动
    if (
      (tempSI >= 65 && tempSI <= 90)
      && (tempSJ < 65 || tempSJ > 90)
    ) {
      i--;
    }
  }
  return newS.join('');
};

console.log(reverseOnlyLetters('ab-cd')); // dc-ba
console.log(reverseOnlyLetters('a-bC-dEf-ghIj')); // j-Ih-gfE-dCba
console.log(reverseOnlyLetters('Test1ng-Leet=code-Q!')); // Qedo1ct-eeLg=ntse-T!
console.log(reverseOnlyLetters('Czyr^')); // ryzC^
```

`node index.js` 返回：

```js
dc-ba
j-Ih-gfE-dCba
Qedo1ct-eeLg=ntse-T!
ryzC^
```

## 四 LeetCode Submit



```js
Accepted
* 116/116 cases passed (72 ms)
* Your runtime beats 27.62 % of javascript submissions
* Your memory usage beats 44.32 % of javascript submissions (33.9 MB)
```

## 五 解题思路



如果你玩过回文串，那么这道题应该手到擒来：

> 暴力破解

```js
const reverseOnlyLetters = (S) => {
  const newS = S.split('');
  const harf = Math.floor(newS.length / 2);
  for (let i = 0, j = newS.length - 1; i < harf, j > i; i++, j--) {
    const tempSI = newS[i].toUpperCase().charCodeAt(),
          tempSJ = newS[j].toUpperCase().charCodeAt();
    // 两边为字母，正常交换
    if (
      (tempSI >= 65 && tempSI <= 90)
      && (tempSJ >= 65 && tempSJ <= 90)
    ) {
      const temp = newS[i];
      newS[i] = newS[j];
      newS[j] = temp;
    }
    // 左侧值异常，右侧值不动
    if (
      (tempSI < 65 || tempSI > 90)
      && (tempSJ >= 65 && tempSJ <= 90)
    ) {
      j++;
    }
    // 右侧值异常，左侧值不动
    if (
      (tempSI >= 65 && tempSI <= 90)
      && (tempSJ < 65 || tempSJ > 90)
    ) {
      i--;
    }
  }
  return newS.join('');
};
```

步骤如下：

1. 拆分 `S` 为数组。
2. 遍历新数组，设置遍历条件 `i, j, harf`。最重要的是，我们需要设置 `j > i`，因为如果不进行设置，那么我们可能会进行 `1 => 2, 2 => 1` 这样的交换操作（坑）。
3. 获取每个字符的 ASCII 值，这里统一转换成大写字母，判断是不是在区间 `[65, 90]` 中即可。
4. 判断两边的值是否都为字母，是的话可以交换操作。
5. 判断左侧值是不是有异常，是的话那么左侧值跳过（`i++, j 不动`）。
6. 判断右侧值是不是有异常，是的话那么右侧值跳过（`j--, i 不动`）。

遍历完毕之后，我们需要将数组转换成字符串进行输出。

Submit 提交如下：

```js
Accepted
* 116/116 cases passed (72 ms)
* Your runtime beats 27.62 % of javascript submissions
* Your memory usage beats 44.32 % of javascript submissions (33.9 MB)
```

## 六 进一步思考



接下来看看大佬们操作：

> 【题解一】双指针

```js
var reverseOnlyLetters = function (S) {
  S = S.split('');
  const { length } = S;
  const reg = /[a-zA-Z]/g;
  for (let i = 0, j = length - 1; i < length; i++) {
    if (S[i].match(reg)) {
      while (j >= 0 && j > i) {
        if (S[j].match(reg)) {
          [S[i], S[j]] = [S[j], S[i]];
          j -= 1;
          break;
        }
        j--
      }
    }
  }
  return S.join('');
};
```

思路和我上面的差不多，如果小伙伴看清楚我上面暴力方法，相信这个也不难~

> 题解中诸多操作，例如 `[S[i], S[j]] = [S[j], S[i]]` 值得学习

Submit 提交如下：

```js
Accepted
* 116/116 cases passed (68 ms)
* Your runtime beats 47.62 % of javascript submissions
* Your memory usage beats 20.45 % of javascript submissions (34.3 MB)
```

> 【题解二】暴力数组

```js
var reverseOnlyLetters = function (S) {
  let arr = S.match(/[a-zA-Z]/g);
  if (arr) {
    arr.reverse();
    for (let i = 0; i < S.length; i++) {
      if (!(/[a-zA-Z]/.test(S[i]))) {
        arr.splice(i, 0, S[i])
      }
    }
  } else {
    arr = S.split('');
  }
  return arr.join('');
};
```

很强，先将字符串提取出来 `S.match`，然后将提取后的数组 `arr` 反转，接着遍历 `S`，将非字母穿插进去。

一气呵成，让人佩服~

Submit 提交：

```js
Accepted
* 116/116 cases passed (68 ms)
* Your runtime beats 47.62 % of javascript submissions
* Your memory usage beats 39.77 % of javascript submissions (34.1 MB)
```

更多的我就不翻题解区了，小伙伴感兴趣的可以自己查找下更优秀的题解。

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

