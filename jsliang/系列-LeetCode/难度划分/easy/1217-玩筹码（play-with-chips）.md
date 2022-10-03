1217 - 玩筹码（play-with-chips）
===

> Create by **jsliang** on **2020-01-31 22:02:45**  
> Recently revised in **2020-01-31 22:25:23**

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
* **涉及知识**：贪心算法、数组、数学
* **题目地址**：https://leetcode-cn.com/problems/play-with-chips/
* **题目内容**：

```
数轴上放置了一些筹码，
每个筹码的位置存在数组 chips 当中。

你可以对 任何筹码 执行下面两种操作之一
（不限操作次数，0 次也可以）：

将第 i 个筹码向左或者右移动 2 个单位，代价为 0。
将第 i 个筹码向左或者右移动 1 个单位，代价为 1。
最开始的时候，同一位置上也可能放着两个或者更多的筹码。

返回将所有筹码移动到同一位置（任意位置）上所需要的最小代价。

示例 1：

输入：chips = [1,2,3]
输出：1
解释：
第二个筹码移动到位置三的代价是 1，
第一个筹码移动到位置三的代价是 0，总代价为 1。

示例 2：

输入：chips = [2,2,2,3,3]
输出：2
解释：
第四和第五个筹码移动到位置二的代价都是 1，
所以最小总代价为 2。

提示：

1 <= chips.length <= 100
1 <= chips[i] <= 10^9

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/play-with-chips
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} chips
 * @return {number}
 */
var minCostToMoveChips = function(chips) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js

```

`node index.js` 返回：

```js

```

## 四 LeetCode Submit



```js

```

## 五 解题思路



是不是没赌过博就看不懂题目，好歹我看过赌圣赌神的电影啊~

在示例 2 中：

```
输入：chips = [2,2,2,3,3]
输出：2
解释：
第四和第五个筹码移动到位置二的代价都是 1，
所以最小总代价为 2。
```

规则：

* 将第 i 个筹码向左或者右移动 2 个单位，代价为 0。
* 将第 i 个筹码向左或者右移动 1 个单位，代价为 1。

第 4 个移动到位置 2 代价是 0，第 5 个移动到位置 2 的代价是 1？

懵圈 ing...

寻思这看下【题解区】吧：

* https://leetcode-cn.com/problems/play-with-chips/solution/zhe-ke-neng-shi-yi-ge-yue-du-li-jie-ti-0ms-by-litt/

```
奇数移动到奇数、偶数移动到偶数是无消耗的，
意思就是算奇数和偶数的个数而已。
```

enm...我……

> 脑经急转弯

```js
const minCostToMoveChips = (chips) => {
  let odd = 0,
      even = 0;
  for (let i = 0; i < chips.length; i++) {
    if (chips[i] % 2 === 0) {
      even++;
    } else {
      odd++;
    }
  }
  return Math.min(even, odd);
};
```

Submit 提交：

```js
Accepted
* 50/50 cases passed (92 ms)
* Your runtime beats 5.98 % of javascript submissions
* Your memory usage beats 35.46 % of javascript submissions (33.8 MB)
```

我，**jsliang**，认输~

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

