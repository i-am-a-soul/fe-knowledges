896 - 单调数列（monotonic-array）
===

> Create by **jsliang** on **2020-1-18 10:17:08**  
> Recently revised in **2020-1-18 11:09:21**

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
* **题目地址**：https://leetcode-cn.com/problems/monotonic-array/
* **题目内容**：

```
如果数组是单调递增或单调递减的，
那么它是单调的。

如果对于所有 i <= j，A[i] <= A[j]，
那么数组 A 是单调递增的。

如果对于所有 i <= j，A[i]> = A[j]，
那么数组 A 是单调递减的。

当给定的数组 A 是单调数组时返回 true，
否则返回 false。

示例 1：

输入：[1,2,2,3]
输出：true

示例 2：

输入：[6,5,4,4]
输出：true

示例 3：

输入：[1,3,2]
输出：false

示例 4：

输入：[1,2,4,5]
输出：true

示例 5：

输入：[1,1,1]
输出：true

提示：

1 <= A.length <= 50000
-100000 <= A[i] <= 100000
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} A
 * @return {boolean}
 */
var isMonotonic = function(A) {

};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 单调数列
 * @param {number[]} A
 * @return {boolean}
 */
const isMonotonic = (A) => Object.assign([], A).sort((a, b) => a - b).join('') === A.join('') || Object.assign([], A).sort((a, b) => b - a).join('') === A.join('');

console.log(isMonotonic([6, 5, 4, 4]));
```

`node index.js` 返回：

```js
true
```

## 四 LeetCode Submit



```js
Accepted
* 366/366 cases passed (452 ms)
* Your runtime beats 5.35 % of javascript submissions
* Your memory usage beats 5.11 % of javascript submissions (71.5 MB)
```

## 五 解题思路



看到题目，我知道又可以秀了，不知道是不是跟我想象中的一样呢？

> 暴力破解

```js
const isMonotonic = (A) => Object.assign([], A).sort((a, b) => a - b).join('') === A.join('') || Object.assign([], A).sort((a, b) => b - a).join('') === A.join('');
```

Submit 提交：

```js
Accepted
* 366/366 cases passed (452 ms)
* Your runtime beats 5.35 % of javascript submissions
* Your memory usage beats 5.11 % of javascript submissions (71.5 MB)
```

想到数组 `sort` 后会改变元素组，所以机智直接浅拷贝了数组 `A`，然后进行顺序和逆序操作，比较原数组 `join('')` 后生成的字符串。

如果两者中有一个对应，那么就是单调数列~

机智，最渣代码诞生~

## 六 进一步思考



细想一下，小优化：

> 暴力小优化 ①

```js
const isMonotonic = (A) => {
  const flag = [];
  for (let i = 0; i < A.length; i++) {
    if (A[i + 1] - A[i] > 0) {
      flag.push(0);
    } else if (A[i + 1] - A[i] < 0) {
      flag.push(1);
    }
  }
  if (flag[0] === 1) {
    return flag.indexOf(0) === -1;
  }
  return flag.indexOf(1) === -1;
};
```

定义一个 `flag`，如果是递减的，那么塞入 `flag` 一个 0，否则塞入一个 1；

最后判断 `flag` 的所有元素是不是和第一个相等即可~

Submit 提交如下：

```js
Accepted
* 366/366 cases passed (96 ms)
* Your runtime beats 36.9 % of javascript submissions
* Your memory usage beats 14.2 % of javascript submissions (41.6 MB)
```

OK，上面用了两次遍历，虽然不是双重 `for` 循环，但是也是挺影响性能的，能不能一次过呢？

> 暴力小优化 ②

```js
const isMonotonic = (A) => {
  let flag;
  for (let i = 0; i < A.length - 1; i++) {
    const result = A[i + 1] - A[i];
    if (result !== 0) {
      if (!flag && result > 0) {
        flag = '单调递增';
      } else if (!flag && result < 0) {
        flag = '单调递减';
      } else if (flag === '单调递增' && result < 0) {
        return false;
      } else if (flag === '单调递减' && result > 0) {
        return false;
      }
    }
  }
  return true;
};
```

思路如下：

1. 判断后一个减去前一个的差值，该差值不为 0 则进一步判断；
2. 判断差值大于 0 并且 `flag` 还没有设置，则是单调递增；
3. 判断差值小于 0 并且 `flag` 还没有设置，则是单调递减；
4. 判断差值大于 0 并且 `flag` 是单调递减，那么返回 `false`，因为它违背了原则；
5. 判断差值小于 0 并且 `flag` 是单调递增，那么返回 `false`，因为它也违背了原则；
6. 其他情况返回 `true` 即可。

Submit 提交：

```js
Accepted
* 366/366 cases passed (84 ms)
* Your runtime beats 85.56 % of javascript submissions
* Your memory usage beats 19.32 % of javascript submissions (41.1 MB)
```

以上，即是 **jsliang** 对这道题的深入剖析，如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

