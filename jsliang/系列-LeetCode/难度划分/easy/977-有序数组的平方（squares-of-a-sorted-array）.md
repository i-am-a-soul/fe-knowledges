977 - 有序数组的平方（squares-of-a-sorted-array）
===

> Create by **jsliang** on **2020-01-28 16:12:04**  
> Recently revised in **2020-01-28 16:21:35**

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
* **涉及知识**：数组、双指针
* **题目地址**：https://leetcode-cn.com/problems/squares-of-a-sorted-array/
* **题目内容**：

```
给定一个按非递减顺序排序的整数数组 A，
返回每个数字的平方组成的新数组，
要求也按非递减顺序排序。 

示例 1：

输入：[-4,-1,0,3,10]
输出：[0,1,9,16,100]

示例 2：

输入：[-7,-3,2,3,11]
输出：[4,9,9,49,121]

提示：

1 <= A.length <= 10000
-10000 <= A[i] <= 10000
A 已按非递减顺序排序。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/squares-of-a-sorted-array
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
var sortedSquares = function(A) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 有序数组的平方
 * @param {number[]} A
 * @return {number[]}
 */
const sortedSquares = (A) => A.map(i => i * i).sort((a, b) => a - b);

console.log(sortedSquares([-4, -1, 0, 3, 10]));
```

`node index.js` 返回：

```js
[ 0, 1, 9, 16, 100 ]
```

## 四 LeetCode Submit



```js
Accepted
* 132/132 cases passed (160 ms)
* Your runtime beats 69.25 % of javascript submissions
* Your memory usage beats 8.57 % of javascript submissions (44.3 MB)
```

## 五 解题思路



太过简单了，我就不逼逼了，上代码：

> 暴力破解【一】

```js
const sortedSquares = (A) => A.map(i => i * i).sort((a, b) => a - b);
```

Submit 提交：

```js
Accepted
* 132/132 cases passed (160 ms)
* Your runtime beats 69.25 % of javascript submissions
* Your memory usage beats 8.57 % of javascript submissions (44.3 MB)
```

> 暴力破解【二】

```js
const sortedSquares = (A) => Array.from(A.map(i => Math.abs(i)).sort((a, b) => a - b), (value) => value * value);
```

多次一举用了 `Array.from`，贪玩了一下。

Submit 提交：

```js
Accepted
* 132/132 cases passed (248 ms)
* Your runtime beats 6.86 % of javascript submissions
* Your memory usage beats 17.96 % of javascript submissions (44 MB)
```

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

> 这题真的提不起兴趣~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

