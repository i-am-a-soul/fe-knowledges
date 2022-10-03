498 - 对角线遍历（diagonal-traverse）
===

> Create by **jsliang** on **2020-07-02 18:10:00**  
> Recently revised in **2020-07-02 18:11:58**  

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
给定一个含有 M x N 个元素的矩阵（M 行，N 列），
请以对角线遍历的顺序返回这个矩阵中的所有元素，
对角线遍历如下图所示。

示例:

输入:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]

输出:  [1,2,4,7,5,3,6,8,9]

说明:

给定矩阵中的元素总数不会超过 100000 。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/diagonal-traverse
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```js
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var findDiagonalOrder = function(matrix) {

};
```

根据上面的已知函数，小伙伴们可以先尝试破解本题，确定了自己的答案后再看下面代码。

## 三 解题思路



```js
const findDiagonalOrder = (matrix) => {
  if (!matrix.length) {
    return [];
  }
  const M = matrix.length; // 横
  const N = matrix[0].length; // 列
  let times = M + N - 1; // 总斜线数
  const result = []; // 结果

  for (let i = 0; i <= times; i++) {
    let count = 0;
    while (count <= i) {
      let [m, n] = [0, 0]; // 横纵坐标
      // 偶数行由右上角到左下角
      if ((i + 1) % 2 === 0) {
        m = count;
        n = i - count;
      } else if ((i + 1) % 2 !== 0) { // 奇数行则相反
        m = i - count;
        n = count;
      }
      // 如果横坐标 m 大于总横数 M
      // 或者纵坐标 n 大于总列数 N
      // 那么就将其中断
      if (m > M - 1 || n > N - 1) {
        count++;
        continue;
      }
      result.push(matrix[m][n]);
      count++;
    }
  }

  return result;
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

