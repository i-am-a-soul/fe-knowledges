1424 - 对角线遍历 II（diagonal-traverse-ii））
===

> Create by **jsliang** on **2020-07-02 18:14:46**  
> Recently revised in **2020-07-02 18:16:28**  

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
给你一个列表 nums ，里面每一个元素都是一个整数列表。

请你依照下面各图的规则，按顺序返回 nums 中对角线上的整数。

示例 1：

输入：nums = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,4,2,7,5,3,8,6,9]

示例 2：

输入：nums = [[1,2,3,4,5],[6,7],[8],[9,10,11],[12,13,14,15,16]]
输出：[1,6,2,8,7,3,9,4,12,10,5,13,11,14,15,16]

示例 3：

输入：nums = [[1,2,3],[4],[5,6,7],[8],[9,10,11]]
输出：[1,4,2,5,3,8,6,9,7,10,11]

示例 4：

输入：nums = [[1,2,3,4,5,6]]
输出：[1,2,3,4,5,6]

提示：

1 <= nums.length <= 10^5
1 <= nums[i].length <= 10^5
1 <= nums[i][j] <= 10^9
nums 中最多有 10^5 个数字。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/diagonal-traverse-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```js
const findDiagonalOrder = (nums) => {

};
```

根据上面的已知函数，小伙伴们可以先尝试破解本题，确定了自己的答案后再看下面代码。

## 三 解题思路



找规律：

```js
const findDiagonalOrder = (nums) => {
  let result = [];
  for (let i = 0; i < nums.length; i++) {
    for (let j = 0; j < nums[i].length; j++) {
      // result 首位追加，这样不需要再次操作数组
      if (result[i + j]) {
        result[i + j].unshift(nums[i][j])
      } else {
        result[i + j] = [nums[i][j]];
      }
    }
  }
  // 数组扁平化
  return result.flat();
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

