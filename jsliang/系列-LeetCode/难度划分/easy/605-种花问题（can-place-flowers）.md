605 - 种花问题（can-place-flowers）
===

> Create by **jsliang** on **2019-11-27 08:38:32**  
> Recently revised in **2019-11-27 09:10:23**

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
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/can-place-flowers/
* **题目内容**：

```
假设你有一个很长的花坛，一部分地块种植了花，另一部分却没有。
可是，花卉不能种植在相邻的地块上，它们会争夺水源，两者都会死去。

给定一个花坛，表示为一个数组包含 0 和 1
其中 0 表示没种植花，1 表示种植了花。

和一个数 n。

能否在不打破种植规则的情况下种入 n 朵花？

能则返回 True，不能则返回 False。

示例 1:

输入: flowerbed = [1,0,0,0,1], n = 1
输出: True

示例 2:

输入: flowerbed = [1,0,0,0,1], n = 2
输出: False

注意:

数组内已种好的花不会违反种植规则。
输入的数组长度范围为 [1, 20000]。
n 是非负整数，且不会超过输入数组的大小。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} flowerbed
 * @param {number} n
 * @return {boolean}
 */
var canPlaceFlowers = function(flowerbed, n) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 种花问题
 * @param {number[]} flowerbed
 * @param {number} n
 * @return {boolean}
 */
const canPlaceFlowers = (flowerbed, n) => {
  let flowers = 0;
  for (let i = 0; i < flowerbed.length; i++) {
    if (
      flowerbed[i] === 0
      && flowerbed[i - 1] !== 1
      && flowerbed[i + 1] !== 1
    ) {
      flowers += 1;
      flowerbed[i] = 1;
    }
    if (flowers >= n) {
      return true;
    }
  }
  return false;
};

console.log(canPlaceFlowers([1, 0, 0, 0, 1], 1)); // true
console.log(canPlaceFlowers([1, 0, 0, 0, 1], 2)); // false
```

`node index.js` 返回：

```js
true
false
```

## 四 LeetCode Submit



```js
Accepted
* 123/123 cases passed (72 ms)
* Your runtime beats 95.68 % of javascript submissions
* Your memory usage beats 73.12 % of javascript submissions (36.1 MB)
```

## 五 解题思路



**首先**，个人思考：

1. `[1, 0, 0, 0, 1]` 的情况，种一朵花可以。
2. `[1, 0, 0, 0, 1]` 的情况，种两朵花不行。

那么，假设有 `[1, 0, 0, 0, 1, 0, 0, 1]` 的情况，能种几朵花？

答案是一朵，**jsliang** 的拆分是：`[1, 0]`、`[0]`、`[0, 1, 0]`、`[0, 1]`。

就是说，一个 `1`，前一个索引或者后一个索引带的值，都会被去掉。

这时候，我们就可以下手了：

> 暴力破解

```js
const canPlaceFlowers = (flowerbed, n) => {
  let flowers = 0;
  for (let i = 0; i < flowerbed.length; i++) {
    if (
      flowerbed[i] === 0
      && flowerbed[i - 1] !== 1
      && flowerbed[i + 1] !== 1
    ) {
      flowers += 1;
      flowerbed[i] = 1;
    }
  }
  return flowers >= n;
};
```

思路非常简单：

1. 设置 `flowers` 为可种植的花朵。
2. 遍历数组，如果数组 `i` 位置的前一个元素和后一个元素均为 0，并且数组 `i` 位置对应的元素也为 0，那么该位置可以种花。
3. 根据步骤 2，我们将 `flowers` 的数量 + 1，同时设置 `flowered[i] = 1`，表明已经种上花了（假设后面也是 0，那么就可以根据前面是否种了新花来判断）
4. 循环数组完毕，判断已种花的数量是否大于或者等于 n，返回结果。

Submit 提交：

```js
Accepted
* 123/123 cases passed (72 ms)
* Your runtime beats 95.68 % of javascript submissions
* Your memory usage beats 70.25 % of javascript submissions (36.1 MB)
```

OK，我们的思路是成功的。

那么，我们还能不能进一步优化？

> 优化暴力破解

```js
const canPlaceFlowers = (flowerbed, n) => {
  let flowers = 0;
  for (let i = 0; i < flowerbed.length; i++) {
    if (
      flowerbed[i] === 0
      && flowerbed[i - 1] !== 1
      && flowerbed[i + 1] !== 1
    ) {
      flowers += 1;
      flowerbed[i] = 1;
    }
    if (flowers >= n) {
      return true;
    }
  }
  return false;
};
```

在这个方法中，我们在 `for` 循环中设置的关卡：

* 当种植的花朵已经足够，那么即可中止函数并且返回 `true`。

这在应对一些特殊情况下是比较满足情况的，因为我们的数组长度范围在 `[1, 20000]`。

如果执行到 `10000` 的时候，发现已经满足种植的花朵数了，我们就不需要继续种植了。

```js
Accepted
* 123/123 cases passed (72 ms)
* Your runtime beats 95.68 % of javascript submissions
* Your memory usage beats 73.12 % of javascript submissions (36.1 MB)
```

当然，这个中止函数的关卡，如果碰到的是非常短的数组，可能比起一开始那个，会损耗一些时间，毕竟 `if` 判断也是需要时间的~

如上，本题解析就此结束。

如果你有更好的思路或者方法，欢迎留言评论或者私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

