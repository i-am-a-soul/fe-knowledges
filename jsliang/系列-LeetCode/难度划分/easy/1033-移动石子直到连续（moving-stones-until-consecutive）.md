1033 - 移动石子直到连续（moving-stones-until-consecutive）
===

> Create by **jsliang** on **2020-01-30 14:26:42**  
> Recently revised in **2020-01-30 15:09:41**

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
* **涉及知识**：脑经急转弯
* **题目地址**：https://leetcode-cn.com/problems/moving-stones-until-consecutive/
* **题目内容**：

```
三枚石子放置在数轴上，
位置分别为 a，b，c。

每一回合，
我们假设这三枚石子当前分别位于位置 x, y, z，
且 x < y < z。
从位置 x 或者是位置 z 拿起一枚石子，
并将该石子移动到某一整数位置 k 处，
其中 x < k < z 且 k != y。

当你无法进行任何移动时，
即，这些石子的位置连续时，游戏结束。

要使游戏结束，你可以执行的最小和最大移动次数分别是多少？
以长度为 2 的数组形式返回答案：
answer = [minimum_moves, maximum_moves]

示例 1：

输入：a = 1, b = 2, c = 5
输出：[1, 2]
解释：将石子从 5 移动到 4 再移动到 3，或者我们可以直接将石子移动到 3。

示例 2：

输入：a = 4, b = 3, c = 2
输出：[0, 0]
解释：我们无法进行任何移动。

提示：

1 <= a <= 100
1 <= b <= 100
1 <= c <= 100
a != b, b != c, c != a

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/moving-stones-until-consecutive
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} a
 * @param {number} b
 * @param {number} c
 * @return {number[]}
 */
var numMovesStones = function(a, b, c) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 移动石子直到连续
 * @param {number} a
 * @param {number} b
 * @param {number} c
 * @return {number[]}
 */
const numMovesStones = (a, b, c) => {
  const sort = [a, b, c].sort((a, b) => a - b);
  [a, b, c] = [sort[0], sort[1], sort[2]];
  // 1. 开场天胡
  if (a + 1 === b && b + 1 === c) {
    return [0, 0];
  } else if (b - a <= 2 || c - b <= 2) { // 2. 挪动 1 个仔即可
    return [1, c - a - 2];
  } else { // 3. 需要挪动 2 个仔
    return [2, c - a - 2];
  }
};

console.log(numMovesStones(1, 2, 5)); // [1, 2]
console.log(numMovesStones(3, 5, 1)); // [1, 2]
```

`node index.js` 返回：

```js
[1, 2]
[1, 2]
```

## 四 LeetCode Submit



```js
Accepted
* 187/187 cases passed (64 ms)
* Your runtime beats 81.54 % of javascript submissions
* Your memory usage beats 71.19 % of javascript submissions (33.7 MB)
```

## 五 解题思路



这个 Tag 打了个 **脑经急转弯**，我是有点措手不及，好像 200 多道题来第一次看到~

而且，坑爹的是它有个 `3 5 1`，提交之后我才发现并不是 `[x, y, z] = [a, b, c]`，而是给出 `a, b, c` 三个数你，你需要先自行排序！

> 脑筋急转弯

```js
const numMovesStones = (a, b, c) => {
  const sort = [a, b, c].sort((a, b) => a - b);
  [a, b, c] = [sort[0], sort[1], sort[2]];
  // 1. 开场天胡
  if (a + 1 === b && b + 1 === c) {
    return [0, 0];
  } else if (b - a <= 2 || c - b <= 2) { // 2. 挪动 1 个仔即可
    return [1, c - a - 2];
  } else { // 3. 需要挪动 2 个仔
    return [2, c - a - 2];
  }
};
```

OK，咱们聊聊做法：

1. 开场天胡的咱们就不多说了，一步都挪不动：`[1, 2, 3]`。这种情况是 `a + 1 = b, b + 1 = c`。
2. 开场地胡的咱们至少可以移动一次，就是：`[1, 3, 4]`。这种情况是 `b - a <= 2, c - b <= 2`。
3. 开场啥都不胡（非酋你好）的咱们辛苦下，至少移动两次，类似：`[1, 5, 8]`。这种情况就排除其他两种情况即可。
4. 那么最多移动多少次？以 `b` 为固定点，结果是：`(b - a - 1) + (c - b - 1)`，所以就是 `c - a - 2` 了。

Submit 提交：

```js
Accepted
* 187/187 cases passed (64 ms)
* Your runtime beats 81.54 % of javascript submissions
* Your memory usage beats 71.19 % of javascript submissions (33.7 MB)
```

OK，搞定完事~

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

