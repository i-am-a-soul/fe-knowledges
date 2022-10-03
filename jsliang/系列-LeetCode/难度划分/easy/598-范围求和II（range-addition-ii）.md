598 - 范围求和II（range-addition-ii）
===

> Create by **jsliang** on **2019-11-25 03:03:45**  
> Recently revised in **2019-11-25 04:08:17**

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题及测试](#chapter-three) |
| [四 LeetCode Submit](#chapter-four) |
| [五 解题思路](#chapter-five) |
| [六 进一步思考](#chapter-six) |

## 二 前言



* **难度**：简单
* **涉及知识**：数学
* **题目地址**：https://leetcode-cn.com/problems/range-addition-ii/
* **题目内容**：

```
给定一个初始元素全部为 0，大小为 m*n 的矩阵 M 以及在 M 上的一系列更新操作。

操作用二维数组表示，
其中的每个操作用一个含有两个正整数 a 和 b 的数组表示，
含义是将所有符合 0 <= i < a 以及 0 <= j < b 的元素 M[i][j] 的值都增加 1。

在执行给定的一系列操作后，你需要返回矩阵中含有最大整数的元素个数。

示例 1:

输入: 
m = 3, n = 3
operations = [[2,2],[3,3]]
输出: 4
解释: 
初始状态, M = 
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]

执行完操作 [2,2] 后, M = 
[[1, 1, 0],
 [1, 1, 0],
 [0, 0, 0]]

执行完操作 [3,3] 后, M = 
[[2, 2, 1],
 [2, 2, 1],
 [1, 1, 1]]

M 中最大的整数是 2, 而且 M 中有4个值为2的元素。因此返回 4。
注意:

m 和 n 的范围是 [1,40000]。
a 的范围是 [1,m]，b 的范围是 [1,n]。
操作数目不超过 10000。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} m
 * @param {number} n
 * @param {number[][]} ops
 * @return {number}
 */
var maxCount = function(m, n, ops) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 范围求和II
 * @param {number} m
 * @param {number} n
 * @param {number[][]} ops
 * @return {number}
 */
const maxCount = (m, n, ops) => {
  const counter = [m, n]; // 横轴，纵轴
  for (let i = 0; i < ops.length; i++) {
    counter[0] = Math.min(counter[0], ops[i][0]);
    counter[1] = Math.min(counter[1], ops[i][1]);
  }
  return counter[0] * counter[1];
};

console.log(maxCount(3, 3, [[2, 2], [3, 3]]));
```

`node index.js` 返回：

```js
4
```

## 四 LeetCode Submit



```js
Accepted
* 69/69 cases passed (68 ms)
* Your runtime beats 60.87 % of javascript submissions
* Your memory usage beats 52.94 % of javascript submissions (35.3 MB)
```

## 五 解题思路



2019-11-25 03:12:49

**首先**，审题，题目表达意思是：

1. 已知参数 `m`, `n`, `ops`。
2. `m * n` 可以构造一个数组 M，是一个由 `m` 行 `n` 列组成的数组。
3. 初始数组的所有元素为 0。
4. 经过 `ops` 的多次渲染后，会逐步加一。
5. 详情如下：

```
输入: 
m = 3, n = 3
operations = [[2,2],[3,3]]

输出: 4

解释: 
初始状态, M = 
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]

执行完操作 [2,2] 后, M = 
[[1, 1, 0],
 [1, 1, 0],
 [0, 0, 0]]

执行完操作 [3,3] 后, M = 
[[2, 2, 1],
 [2, 2, 1],
 [1, 1, 1]]

M 中最大的整数是 2, 而且 M 中有4个值为2的元素。因此返回 4。
```

那么，搞懂题目想要什么的情况下，我们需要注意它下面写的东西：

1. `m` 和 `n` 的范围是 `[1,40000]`。
2. `a` 的范围是 `[1,m]`，`b` 的范围是 `[1,n]`。
3. 操作数目不超过 `10000`。

往往很多时候，我们题目是解出来了，但是超时了。

暴力虽好，但是对一个二维数组进行 10000 次的暴力，那就是残忍。

**然后**，分析完毕，开始解题：

```js
const maxCount = (m, n, ops) => {
  const counter = [m, n]; // 横轴，纵轴
  for (let i = 0; i < ops.length; i++) {
    counter[0] = Math.min(counter[0], ops[i][0]);
    counter[1] = Math.min(counter[1], ops[i][1]);
  }
  return counter[0] * counter[1];
};

console.log(maxCount(3, 3, [[2, 2], [3, 3]]));
```

Submit 提交：

```js
Accepted
* 69/69 cases passed (68 ms)
* Your runtime beats 60.87 % of javascript submissions
* Your memory usage beats 52.94 % of javascript submissions (35.3 MB)
```

Perfect!

证明我们的思路是没错的：

1. 每次渲染的时候，`a` 的范围是 `[1, m]`，`b` 的范围是 `[1, n]`，证明数组至少有 1 * 1 = 1 个是会被渲染增加为最大整数的。
2. 这时候，我们只需要知道它遍历了多少次 `ops.length`，然后将这些遍历中重叠的范围找出来即可。

| 0 | 0 | 0 |
| --- | --- | ---|
| 0 | 0 | 0 |
| 0 | 0 | 0 |

假设数组如上：3 * 3（m * n）

然后 `ops` 为 `[[1, 3], [2, 2]]`。

那么第一次渲染 `[1, 3]` 后：

| 1 | 1 | 1 |
| --- | --- | ---|
| 0 | 0 | 0 |
| 0 | 0 | 0 |

第二次渲染 `[2, 2]` 后：

| 2 | 2 | 1 |
| --- | --- | ---|
| 1 | 1 | 0 |
| 0 | 0 | 0 |

很容易发现，最终的数量是 2 个，怎么来的呢？

* 横轴：最小值为 `Math.min(1, 2)`。即 `ops[i][0]`
* 纵轴：最小值为 `Math.min(3, 2)`。即 `ops[i][1]`
* 结果：横轴最小值 * 纵轴最小值。

这样，我们就完成了题目的破解啦！

## 六 进一步思考



今天的进一步思考，主要是讲解为什么有时候暴力不好使：

> 暴力破解

```js
/**
 * @name 范围求和II
 * @param {number} m
 * @param {number} n
 * @param {number[][]} ops
 * @return {number}
 */
const maxCount = (m, n, ops) => {
  if (!ops.length) {
    return m * n;
  }
  const list = [];
  for (let i = 0; i < m; i++) {
    list[i] = [];
    for (let j = 0; j < n; j++) {
      list[i][j] = 0;
    }
  }
  const counter = [1, 0]; // 最大值, 元素个数
  for (let k = 0; k < ops.length; k++) {
    for (let i = 0; i < ops[k][0]; i++) {
      for (let j = 0; j < ops[k][1]; j++) {
        list[i][j] += 1;
        if (list[i][j] === counter[0]) {
          counter[1] += 1;
        }
        if (list[i][j] > counter[0]) {
          counter[0] = list[i][j];
          counter[1] = 1;
        }
      }
    }
  }
  console.log(list);
  return counter[1];
};

console.log(maxCount(3, 3, [[2, 2], [3, 3]]));
```

这种解法，在碰到 `maxCount(39999, 39999, [[19999, 19999]])` 这种情况的时候，无疑直接炸锅：

```js
Runtime Error
7/69 cases passed (N/A)

Testcase
39999
39999
[[19999,19999]]
```

就好比妹子跟你约好 15:00 见面，然后你打了个游戏 03:00 再去找她一样~

至于更深层次的，希望小伙伴能进一步思考探索啦~

如果你有更好的思路或者方法，欢迎留言评论或者私聊 **jsliang**。

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

