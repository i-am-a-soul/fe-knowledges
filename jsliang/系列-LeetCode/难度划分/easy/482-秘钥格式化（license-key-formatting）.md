482 - 秘钥格式化（license-key-formatting）
===

> Create by **jsliang** on **2019-10-26 16:04:27**  
> Recently revised in **2019-10-26 17:05:48**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题及测试](#chapter-three) |
| [四 LeetCode Submit](#chapter-four) |
| [五 解题思路](#chapter-five) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：数组、字符串
* **题目地址**：https://leetcode-cn.com/problems/license-key-formatting/
* **题目内容**：

```
给定一个密钥字符串S，只包含字母，数字以及 '-'（破折号）。

N 个 '-' 将字符串分成了 N+1 组。

给定一个数字 K，重新格式化字符串。

除了第一个分组以外，每个分组要包含 K 个字符。

第一个分组至少要包含 1 个字符。

两个分组之间用 '-'（破折号）隔开，并且将所有的小写字母转换为大写字母。

给定非空字符串 S 和数字 K，按照上面描述的规则进行格式化。

示例 1：

输入：S = "5F3Z-2e-9-w", K = 4
输出："5F3Z-2E9W"
解释：字符串 S 被分成了两个部分，每部分 4 个字符；
     注意，两个额外的破折号需要删掉。

示例 2：
输入：S = "2-5g-3-J", K = 2
输出："2-5G-3J"
解释：字符串 S 被分成了 3 个部分，按照前面的规则描述。
第一部分的字符可以少于给定的数量，其余部分皆为 2 个字符。

提示:

S 的长度不超过 12,000，K 为正整数
S 只包含字母数字（a-z，A-Z，0-9）以及破折号'-'
S 非空
```

## <a name="chapter-three" id="chapter-three">三 解题及测试</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} S
 * @param {number} K
 * @return {string}
 */
var licenseKeyFormatting = function(S, K) {
  
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 秘钥格式化
 * @param {string} S
 * @param {number} K
 * @return {string}
 */
const licenseKeyFormatting = (S, K) => {
  S = S.split('').filter(i => i !== '-').join('').toUpperCase();

  let result = '';
  for (let i = S.length - 1, j = 1; i >= 0; i--, j++) {
    result = S[i] + result;
    if (j === K && i !== 0) {
      result = '-' + result;
      j = 0;
    }
  }
  return result;
};

// const S = '2-5g-3-J';
// const K = 2;
const S = '5F3Z-2e-9-w';
const K = 4;
console.log(licenseKeyFormatting(S, K));
```

`node index.js` 返回：

```js
5F3Z-2E9W
```

## <a name="chapter-four" id="chapter-four">四 LeetCode Submit</a>



```js
Accepted
* 38/38 cases passed (76 ms)
* Your runtime beats 84.81 % of javascript submissions
* Your memory usage beats 55.56 % of javascript submissions (41.1 MB)
```

## <a name="chapter-five" id="chapter-five">五 解题思路</a>



初始审题，尚未睡醒，信手拿来：

```js
/**
 * @name 秘钥格式化
 * @param {string} S
 * @param {number} K
 * @return {string}
 */
const licenseKeyFormatting = (S, K) => {
  S = S.split('').filter(i => i !== '-').join('');
  let result = '';
  for (let i = 0; i < S.length; i++) {
    if ((i + 1) % K === 0 && (i + 1) != S.length) {
      result = result + S[i] + '-';
    } else {
      result += S[i];
    }
  }
  return result.toUpperCase();
};
```

Submit 后立马暴毙：

```js
Testcase
"2-5g-3-J"
2

Answer
"25-G3-J"

Expected Answer
"2-5G-3J"
```

所以，我还需要考虑第一个分组：

1. 第一个分组的长度小于或者等于 K，则第一个分组不动
2. 第一个分组的长度大于 K，则缩小为 K 的长度

于是写下：

```js
/**
 * @name 秘钥格式化
 * @param {string} S
 * @param {number} K
 * @return {string}
 */
const licenseKeyFormatting = (S, K) => {
  let result = '';
  // 切割第一个分组
  const firstLength = S.split('-')[0].length;
  // 切割第二个及以上分组
  let start = 0;
  if (firstLength <= K) {
    start = firstLength;
  } else {
    start = K;
  }
  S = S.split('').filter(i => i !== '-').join('').toUpperCase();
  result = result + S.slice(0, start) + '-';
  for (let i = start; i < S.length; i++) {
    result += S[i];
    if ((i + 1 - start) % K === 0 && (i + 1) != S.length) {
      result += '-';
    }
  }
  return result;
};
```

Submit 提交：

```js
Testcase
"2-4A0r7-4k"
4

Answer
"2-4A0R-74K"

Expected Answer
"24A0-R74K"
```

看到这里，我就明白了，它想要我死……吧

再度审了一遍题，猜测它其实想要的是我倒着分组，这样排在前面的，要不就符合 K 以下长度（包含 K 长度），要不就是小于 K 长度，于是不甘心将上面代码删了再试试：

```js
/**
 * @name 秘钥格式化
 * @param {string} S
 * @param {number} K
 * @return {string}
 */
const licenseKeyFormatting = (S, K) => {
  S = S.split('').filter(i => i !== '-').join('').toUpperCase();

  let result = '';
  for (let i = S.length - 1, j = 1; i >= 0; i--, j++) {
    result = S[i] + result;
    if (j === K && i !== 0) {
      result = '-' + result;
      j = 0;
    }
  }
  return result;
};
```

Submit 提交：

```js
Accepted
38/38 cases passed (84 ms)
Your runtime beats 69.62 % of javascript submissions
Your memory usage beats 48.15 % of javascript submissions (41.3 MB)
```

搞定！果然我还是没睡醒~

如果你有更好解题方式，欢迎留言~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

