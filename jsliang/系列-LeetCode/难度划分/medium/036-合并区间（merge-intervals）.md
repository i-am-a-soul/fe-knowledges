036 - 合并区间（merge-intervals）
===

> Create by **jsliang** on **2020-07-02 17:48:48**  
> Recently revised in **2020-07-02 17:50:11**  

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- |
| [一 目录](#chapter-one) |
| [二 题目](#chapter-two) |
| [三 解题思路](#chapter-three) |
| [四 统计分析](#chapter-four) |
| [五 解题套路](#chapter-five) |

## 二 题目



```
给出一个区间的集合，请合并所有重叠的区间。

示例 1:

输入: [[1,3],[2,6],[8,10],[15,18]]
输出: [[1,6],[8,10],[15,18]]
解释: 区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].

示例 2:

输入: [[1,4],[4,5]]
输出: [[1,5]]
解释: 区间 [1,4] 和 [4,5] 可被视为重叠区间。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/merge-intervals
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```js
/**
 * @param {number[][]} intervals
 * @return {number[][]}
 */
var merge = function(intervals) {

};
```

根据上面的已知函数，小伙伴们可以先尝试破解本题，确定了自己的答案后再看下面代码。

## 三 解题思路



先通过 `sort()` 排序，然后判断查找即可：

```js
/**
 * 疑问：
 1. 这个数组有序吗？[[4,5],[1,4]]。答：无序
 2. 这个数组元素重叠怎么算？[[1,4],[4,5]]。答：合并
*/
const merge = (intervals) => {
  intervals.sort((a, b) => a[0] - b[0]);
  for (let i = 0; i < intervals.length - 1; i++) {
    const left = intervals[i];
    const right = intervals[i + 1];
    if (
      left[1] >= right[0] && left[1] <= right[1]
      || (right[0] >= left[0] && right[0] <= left[1])
    ) {
      intervals.splice(i, 2, [Math.min(left[0], right[0]), Math.max(left[1], right[1])]);
      i--;
    }
  }
  return intervals;
};
```

## 四 统计分析



本题不需要统计分析。

## 五 套路分析



本题暂未发现任何套路，如果有但是 **jsliang** 后面发现了的话，会在 GitHub 进行补充。

如果小伙伴有更好的思路想法，或者没看懂其中某种解法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](https://github.com/LiangJunrong/document-library/blob/master/public-repertory/img/z-index-small.png?raw=true)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

