1046 - 最后一块石头的重量（last-stone-weight）
===

> Create by **jsliang** on **2020-01-30 20:56:12**  
> Recently revised in **2020-01-30 21:21:21**

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
* **涉及知识**：堆、贪心算法
* **题目地址**：https://leetcode-cn.com/problems/last-stone-weight/
* **题目内容**：

```
有一堆石头，
每块石头的重量都是正整数。

每一回合，
从中选出两块最重的石头，
然后将它们一起粉碎。

假设石头的重量分别为 x 和 y，
且 x <= y。

那么粉碎的可能结果如下：

如果 x == y，那么两块石头都会被完全粉碎；
如果 x != y，那么重量为 x 的石头将会完全粉碎，
而重量为 y 的石头新重量为 y-x。
最后，最多只会剩下一块石头。返回此石头的重量。
如果没有石头剩下，就返回 0。

提示：

1 <= stones.length <= 30
1 <= stones[i] <= 1000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/last-stone-weight
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} stones
 * @return {number}
 */
var lastStoneWeight = function(stones) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 最后一块石头的重量
 * @param {number[]} stones
 * @return {number}
 */
const lastStoneWeight = (stones) => {
  stones.sort((a, b) => a - b);
  while (stones.length > 1) {
    const one = stones.pop();
    const two = stones.pop();
    if (one - two !== 0) {
      stones.push(one - two);
      stones.sort((a, b) => a - b);
    }
  }
  return stones[0] || 0;
};

console.log(lastStoneWeight([2, 3, 4])) // 1
```

`node index.js` 返回：

```js
1
```

## 四 LeetCode Submit



```js
Accepted
* 70/70 cases passed (68 ms)
* Your runtime beats 78.24 % of javascript submissions
* Your memory usage beats 83.33 % of javascript submissions (34.6 MB)
```

## 五 解题思路



LeetCode 越来越过分了：

1. 第 1000 题之后，官方题解基本不写。
2. 第 1042 题的 图（Tag），让我搞了 3 个多钟。
3. 到了第 1046 这道题，连示例都不写了。
4. ……

LeetCode 你变了~

重构题目：

---
参数：

* stones：[2, 3, 3]。有一堆石头，它的范围是 [1, 30]，并且里面每个值大小是 [1, 1000]。

内容：

1. 每次遍历，先挑选两块最重的石头 x 和 y（数字最大的前两块），x <= y，让它们进行互相碾压。
2. 如果两块石头重量一样，那么它们都变成了渣渣，消失于 `stones` 中。
3. 如果这两块石头重量不一样，那么较大的那块会剩下 `y - x` 的渣渣，然后这个渣渣重新加入 `stones` 大家庭中。
4. 碾压到剩下一块石头为止，胜者为王！返回它的重量！
---

OK，咱们开始拿几个例子看看：

> 示例 1

```
输入：[2, 3, 3]
输出：2
解释：3 和 3 同归于尽，剩下 2
```

> 示例 2

```
输入：[2, 3, 4]
输出：1
解释：4 和 3 互相碾压变成 1，2 和 1 互相碾压剩下 1
```

这样，我们就可以得出答案：

> 暴力破解

```js
const lastStoneWeight = (stones) => {
  stones.sort((a, b) => a - b);
  while (stones.length > 1) {
    const one = stones.pop();
    const two = stones.pop();
    if (one - two !== 0) {
      stones.push(one - two);
      stones.sort((a, b) => a - b);
    }
  }
  return stones[0] || 0;
};
```

Submit 提交：

```js
Accepted
* 70/70 cases passed (68 ms)
* Your runtime beats 78.24 % of javascript submissions
* Your memory usage beats 83.33 % of javascript submissions (34.6 MB)
```

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

