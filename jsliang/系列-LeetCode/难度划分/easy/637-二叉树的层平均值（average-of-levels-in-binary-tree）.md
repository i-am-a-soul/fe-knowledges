637 - 二叉树的层平均值（average-of-levels-in-binary-tree）
===

> Create by **jsliang** on **2019-12-02 08:44:06**  
> Recently revised in **2019-12-02 09:42:51**

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
* **涉及知识**：树
* **题目地址**：https://leetcode-cn.com/problems/average-of-levels-in-binary-tree/
* **题目内容**：

```
给定一个非空二叉树, 返回一个由每层节点平均值组成的数组.

示例 1:

输入:
    3
   / \
  9  20
    /  \
   15   7

输出: [3, 14.5, 11]

解释:
第 0 层的平均值是 3, 
第 1 层是 14.5, 
第 2 层是 11. 
因此返回 [3, 14.5, 11]。

注意：

节点值的范围在32位有符号整数范围内。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var islandPerimeter = function(grid) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @name 二叉树的层平均值
 * @param {TreeNode} root
 * @return {number[]}
 */
const averageOfLevels = (root) => {
  const result = [];
  const traverse = (root, depth) => {
    if (!root) {
      return;
    }
    (result[depth] || (result[depth] = [])).push(root.val);
    traverse(root.left, depth + 1);
    traverse(root.right, depth + 1);
  };
  traverse(root, 0);
  return result.map(item => item.reduce((pre, cur) => pre + cur) / item.length);
};

// const root = {
//   val: 3,
//   left: { val: 9, left: null, right: null },
//   right: {
//     val: 20,
//     left: { val: 15, left: null, right: null },
//     right: { val: 7, left: null, right: null },
//   },
// };
// [ 3, 14.5, 11 ]

const root = {
  val: 3,
  left: {
    val: 1,
    left: { val: 0, left: null, right: null },
    right: { val: 2, left: null, right: null },
  },
  right: {
    val: 5,
    left: { val: 4, left: null, right: null },
    right: { val: 6, left: null, right: null },
  },
};
// [ 3, 3, 3 ]

// const root = {
//   val: -40,
//   left: { val: 0, left: null, right: null },
//   right: { val: -37, left: null, right: null },
// };
// [-40, -18.5]

console.log(averageOfLevels(root));
```

`node index.js` 返回：

```js
[ 3, 3, 3 ]
```

## 四 LeetCode Submit



```js
Accepted
* 65/65 cases passed (68 ms)
* Your runtime beats 99.12 % of javascript submissions
* Your memory usage beats 79.41 % of javascript submissions (38 MB)
```

## 五 解题思路



**原以为是简单难度，谁知死在测试用例上**。

直接上代码：

> 第一次题解

```js
const averageOfLevels = (root) => {
  const treeList = [];
  const map = new Map();
  const ergodic = (root, deep) => {
    if (!root) {
      return;
    }
    if (treeList[deep]) {
      treeList[deep] = (treeList[deep] + root.val) / map.get(deep);
      map.set(deep, map.get(deep) + 1);
    } else {
      treeList[deep] = root.val;
      map.set(deep, 2);
    }
    deep += 1;
    return ergodic(root.left, deep) + ergodic(root.right, deep);
  };
  ergodic(root, 0);
  return treeList;
};
```

1. 通过 `treeList` 记录最终结果
2. 通过 `map` 记录该层出现的次数
3. 通过 `ergodic` 进行递归
4. 递归中。如果节点为空，直接返回
5. 递归中。如果 `treeList` 的该层 `deep` 位置不存在，则添加该元素；否则将它的值加上 `root.val`，并处于 `map` 中记录该位置所出现的次数
6. 递归中。每次非空节点的遍历，都将 `deep` 的层次加一，直至递归结束
7. 最后返回结果 `treeList`

但是！还是出问题了：

```js
Wrong Answer
61/65 cases passed (N/A)

Testcase
[-40,0,-37,17,-87, ...省略..., null,null,3]

Answer
[-40.0,-37.0,11.5, ...省略..., -15.48889,3.0]

Expected Answer
[-40.0,-18.5,-5.25, ...省略..., -26.83333,3.0]
```

瞬间懵逼，这场景是什么鬼，我要怎么复现出来？

于是我去【题解区】找了一个：

> 参照题解

```js
const averageOfLevels = (root) => {
  const res = [];
  if (!root) return res;
  const traverse = (node, depth) => {
    (res[depth] || (res[depth] = [])).push(node.val);
    if (node.left) traverse(node.left, depth + 1);
    if (node.right) traverse(node.right, depth + 1);
  };
  traverse(root, 0);
  return res.map(item => item.reduce((pre, cur) => pre + cur) / item.length);
};
```

Submit 提交：

```js
Accepted
* 65/65 cases passed (92 ms)
* Your runtime beats 50 % of javascript submissions
* Your memory usage beats 94.12 % of javascript submissions (37.8 MB)
```

纳闷，回头再看看 `Map` 记录：

```js
Map {
  0 => 2,
  1 => 2,
  2 => 5,
  3 => 9,
  4 => 17,
  5 => 29,
  6 => 42,
  7 => 70,
  8 => 90,
  9 => 99,
  10 => 98,
  11 => 88,
  12 => 89,
  13 => 88,
  14 => 73,
  15 => 64,
  16 => 55,
  17 => 50,
  18 => 29,
  19 => 13,
  20 => 7,
  21 => 2 }
```

究竟哪里有问题？难不成是我 JS 被诟病的加减乘除计算？也不对啊！

仔细观察，第 1 层的时候有两个值，然后对应的是：

```js
const root = {
  val: -40,
  left: { val: 0, left: null, right: null },
  right: { val: -37, left: null, right: null },
};
```

问题很大啊兄嘚，遍历第 1 层的时候 `treeList[1] = 0`，然后就判断没了啊，所以最终结果是 `37`。

还有就是，每次我都会除于一个平均值，这就很大问题了：导致累计之后数值不准，所以还是需要使用 **参照题解**，才是上佳选择。

如上，如果小伙伴有更好的思路或者解法，欢迎评论留言或者私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

