922 - 按奇偶排序数组II（sort-array-by-parity-ii）
===

> Create by **jsliang** on **2020-01-24 18:53:29**  
> Recently revised in **2020-01-24 19:26:30**

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
* **涉及知识**：排序、数组
* **题目地址**：https://leetcode-cn.com/problems/sort-array-by-parity-ii/
* **题目内容**：

```
给定一个非负整数数组 A，
A 中一半整数是奇数，
一半整数是偶数。

对数组进行排序，
以便当 A[i] 为奇数时，
i 也是奇数；
当 A[i] 为偶数时，
i 也是偶数。

你可以返回任何满足上述条件的数组作为答案。

示例：

输入：[4,2,5,7]
输出：[4,5,2,7]
解释：[4,7,2,5]，[2,5,4,7]，[2,7,4,5] 也会被接受。

提示：

2 <= A.length <= 20000
A.length % 2 == 0
0 <= A[i] <= 1000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/sort-array-by-parity-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} A
 * @return {number[]}
 */
var sortArrayByParityII = function(A) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 按奇偶排序数组
 * @param {number[]} A
 * @return {number[]}
 */
const sortArrayByParityII = (A) => {
  const jishu = [],
        oushu = [];
  for (let i = 0; i < A.length; i++) {
    if (A[i] % 2 === 0) {
      oushu.push(A[i]);
    } else {
      jishu.push(A[i]);
    }
  }
  const result = [];
  for (let i = 0; i < A.length; i++) {
    if (i % 2 === 0) {
      result.push(oushu.pop());
    } else {
      result.push(jishu.pop());
    }
  }
  return result;
};

console.log(sortArrayByParityII([4, 2, 5, 7]));
```

`node index.js` 返回：

```js
[ 2, 7, 4, 5 ]
```

## 四 LeetCode Submit



```js
Accepted
* 61/61 cases passed (124 ms)
* Your runtime beats 44.81 % of javascript submissions
* Your memory usage beats 17.01 % of javascript submissions (41.7 MB)
```

## 五 解题思路



如果你做过 905，那么这道题应该也不是问题，先上白痴操作：

> 暴力破解 1

```js
const sortArrayByParityII = (A) => {
  const jishu = [],
        oushu = [];
  for (let i = 0; i < A.length; i++) {
    if (A[i] % 2 === 0) {
      oushu.push(A[i]);
    } else {
      jishu.push(A[i]);
    }
  }
  const result = [];
  for (let i = 0; i < A.length; i++) {
    if (i % 2 === 0) {
      result.push(oushu.pop());
    } else {
      result.push(jishu.pop());
    }
  }
  return result;
};
```

这种解法思路简单：

1. 设置 `jishu` 获取奇数对应的数组，设置 `oushu` 获取偶数对应的数组。（偷懒我就不翻译成英文了好吧）
2. 遍历一次 `A` 数组，将奇偶进行归类。
3. 再遍历一次 `A` 数组，按奇偶位置将值放到 `result` 中。
4. 返回最终结果 `result`。

Submit 提交如下：

```js
Accepted
* 61/61 cases passed (124 ms)
* Your runtime beats 44.81 % of javascript submissions
* Your memory usage beats 17.01 % of javascript submissions (41.7 MB)
```

## 六 进一步思考



当然，仔细思考还有其他法子的：

> 暴力破解 2

```js
const sortArrayByParityII = (A) => {
  const result = new Array(A.length).fill('');
  let oushu = 0, jishu = 1;
  while (A.length > 0) {
    const temp = A.pop();
    if (temp % 2 === 0) {
      result[oushu] = temp;
      oushu += 2;
    } else {
      result[jishu] = temp;
      jishu += 2;
    }
  }
  return result;
};
```

1. 新建一个空数组，用 `''` 初始化每一项；
2. 遍历 `A` 的长度，不停 `pop` 它每一项元素；
3. 将偶数的放到偶数位，将奇数的放到奇数位。

搞定，收工~

Submit 提交：

```js
Accepted
* 61/61 cases passed (116 ms)
* Your runtime beats 71.21 % of javascript submissions
* Your memory usage beats 65.42 % of javascript submissions (39.2 MB)
```

当然，以上是 **jsliang** 个人拙劣见解，如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~
 
---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

