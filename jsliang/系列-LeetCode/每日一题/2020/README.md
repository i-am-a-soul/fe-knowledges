LeetCode 2020 每日一题
===

> Create by **jsliang** on **2020-07-03 13:45:10**  
> Recently revised in **2020-07-09 11:29:59**  

有小伙伴好奇：

* **jsliang** 又拖更偷懒了！

其实，真不是。

1. 重写了书籍关于《算法与数据结构 - 数组》的部分。
2. 跟进了 LeetCode 官方的每日一题。

> 每日一题地址：https://leetcode-cn.com/circle/article/9EZfRE/?utm_campaign=daily_question&utm_medium=banner&utm_source=problemset&gio_link_id=noqw6arR

闲话不哆嗦，今天就分享一道 2 分钟能破解的题吧：

```
给定一个 n x n 矩阵，其中每行和每列元素均按升序排序，
找到矩阵中第 k 小的元素。

请注意，它是排序后的第 k 小元素，而不是第 k 个不同的元素。

示例：

matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

返回 13。
 

提示：
你可以假设 k 的值永远是有效的，1 ≤ k ≤ n2 。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```js
/**
 * @param {number[][]} matrix
 * @param {number} k
 * @return {number}
 */
var kthSmallest = function(matrix, k) {

};
```

它简单在哪呢？

**jsliang** 看了 2 分钟题目，然后花了 20 秒写出答案：

```js
const kthSmallest = (matrix, k) => matrix.flat().sort((a, b) => a - b)[k - 1];
```

这是一道中等难度的题目，但是破解的方法简单地不能再简单。

被震惊到的请留言，哈哈！

截至今天每日一题更新内容有：

* 0701-718-最长重复子数组
* 0702-378-有序矩阵中第K小的元素
* 0703-108-将有序数组转换为二叉搜索树
* 0706-63-不同路径II
* 0707-112-路径总和
* 0708-面试题16.11-跳水板
* 0709-面试题17.13-恢复空格

如果你也想每日打卡，这个就合适了，可以适当保持你的刷题状态。

> 又水了一篇文章

---

**不折腾的前端，和咸鱼有什么区别！**

![图](https://github.com/LiangJunrong/document-library/blob/master/public-repertory/img/z-index-small.png?raw=true)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

