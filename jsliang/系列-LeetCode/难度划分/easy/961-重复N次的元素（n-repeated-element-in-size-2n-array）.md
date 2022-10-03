961 - 重复N次的元素（n-repeated-element-in-size-2n-array）
===

> Create by **jsliang** on **2020-01-28 11:06:31**  
> Recently revised in **2020-01-28 11:22:36**

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
* **涉及知识**：哈希表
* **题目地址**：https://leetcode-cn.com/problems/n-repeated-element-in-size-2n-array/
* **题目内容**：

```
在大小为 2N 的数组 A 中有 N+1 个不同的元素，
其中有一个元素重复了 N 次。

返回重复了 N 次的那个元素。

示例 1：

输入：[1,2,3,3]
输出：3

示例 2：

输入：[2,1,2,5,3,2]
输出：2

示例 3：

输入：[5,1,5,2,5,3,5,4]
输出：5 

提示：

4 <= A.length <= 10000
0 <= A[i] < 10000
A.length 为偶数

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/n-repeated-element-in-size-2n-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} A
 * @return {number}
 */
var repeatedNTimes = function(A) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 重复N次的元素
 * @param {number[]} A
 * @return {number}
 */
const repeatedNTimes = (A) => {
  for (let i = 0; i < A.length; i++) {
    if (A.indexOf(A[i]) !== A.lastIndexOf(A[i])) {
      return A[i];
    }
  }
};

console.log(repeatedNTimes([2, 1, 2, 5, 3, 2])); // 2
```

`node index.js` 返回：

```js
2
```

## 四 LeetCode Submit



```js
Accepted
* 102/102 cases passed (72 ms)
* Your runtime beats 82.72 % of javascript submissions
* Your memory usage beats 56.5 % of javascript submissions (36.8 MB)
```

## 五 解题思路



经过前面题目的摧残，看到这道题我有点怀疑自己眼光，是不是看错了，结果还真是这样：

> 【解法一】indexOf & lastIndexOf

```js
const repeatedNTimes = (A) => {
  for (let i = 0; i < A.length; i++) {
    if (A.indexOf(A[i]) !== A.lastIndexOf(A[i])) {
      return A[i];
    }
  }
};
```

enm...Submit 提交：

```js
Accepted
* 102/102 cases passed (72 ms)
* Your runtime beats 82.72 % of javascript submissions
* Your memory usage beats 56.5 % of javascript submissions (36.8 MB)
```

这样子的话，我可以变着法子虐他啊！

先用 `Map`：

> 【解法二】Map

```js
const repeatedNTimes = (A) => {
  const map = new Map();
  for (let i = 0; i < A.length; i++) {
    if (map.get(A[i])) {
      return A[i];
    }
    map.set(A[i], 'jsliang');
  }
};
```

Submit 提交：

```js
Accepted
* 102/102 cases passed (72 ms)
* Your runtime beats 82.72 % of javascript submissions
* Your memory usage beats 69.5 % of javascript submissions (36.3 MB)
```

再用 `Array`：

> 【解法三】Array

```js
const repeatedNTimes = (A) => {
  const arr = [];
  for (let i = 0; i < A.length; i++) {
    if (arr[A[i]] !== undefined) {
      return A[i];
    }
    arr[A[i]] = A[i];
  }
};
```

Submit 提交：

```js
Accepted
* 102/102 cases passed (72 ms)
* Your runtime beats 82.72 % of javascript submissions
* Your memory usage beats 96.5 % of javascript submissions (36.1 MB)
```

最后我就不再探索啦，太过简单了，不想瞅瞅其他大佬的答案了~

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

