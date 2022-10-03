558 - 四叉树交集（quad-tree-intersection）
===

> Create by **jsliang** on **2019-11-14 08:42:39**  
> Recently revised in **2019-11-15 08:34:55**

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
* **题目地址**：https://leetcode-cn.com/problems/quad-tree-intersection/
* **题目内容**：

```
四叉树是一种树数据，其中每个结点恰好有四个子结点：
  topLeft、topRight、bottomLeft 和 bottomRight。
  
四叉树通常被用来划分一个二维空间，递归地将其细分为四个象限或区域。

我们希望在四叉树中存储 True/False 信息。

四叉树用来表示 N * N 的布尔网格。

对于每个结点, 它将被等分成四个孩子结点直到这个区域内的值都是相同的。

每个节点都有另外两个布尔属性：isLeaf 和 val。

当这个节点是一个叶子结点时 isLeaf 为真。

val 变量储存叶子结点所代表的区域的值。

例如，下面是两个四叉树 A 和 B：

A:
+-------+-------+   T: true
|       |       |   F: false
|   T   |   T   |
|       |       |
+-------+-------+
|       |       |
|   F   |   F   |
|       |       |
+-------+-------+
topLeft: T
topRight: T
bottomLeft: F
bottomRight: F

B:               
+-------+---+---+
|       | F | F |
|   T   +---+---+
|       | T | T |
+-------+---+---+
|       |       |
|   T   |   F   |
|       |       |
+-------+-------+
topLeft: T
topRight:
     topLeft: F
     topRight: F
     bottomLeft: T
     bottomRight: T
bottomLeft: T
bottomRight: F
 

你的任务是实现一个函数

该函数根据两个四叉树返回表示这两个四叉树的逻辑或(或并)的四叉树。

A:                 B:                 C (A or B):
+-------+-------+  +-------+---+---+  +-------+-------+
|       |       |  |       | F | F |  |       |       |
|   T   |   T   |  |   T   +---+---+  |   T   |   T   |
|       |       |  |       | T | T |  |       |       |
+-------+-------+  +-------+---+---+  +-------+-------+
|       |       |  |       |       |  |       |       |
|   F   |   F   |  |   T   |   F   |  |   T   |   F   |
|       |       |  |       |       |  |       |       |
+-------+-------+  +-------+-------+  +-------+-------+
 

提示：

A 和 B 都表示大小为 N * N 的网格。
N 将确保是 2 的整次幂。

如果你想了解更多关于四叉树的知识，
你可以参考 https://en.wikipedia.org/wiki/Quadtree 这个页面。

逻辑或的定义如下：
如果 A 为 True ，
或者 B 为 True ，
或者 A 和 B 都为 True，
则 "A 或 B" 为 True。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * // Definition for a QuadTree node.
 * function Node(val,isLeaf,topLeft,topRight,bottomLeft,bottomRight) {
 *    this.val = val;
 *    this.isLeaf = isLeaf;
 *    this.topLeft = topLeft;
 *    this.topRight = topRight;
 *    this.bottomLeft = bottomLeft;
 *    this.bottomRight = bottomRight;
 * };
 */
/**
 * @param {Node} quadTree1
 * @param {Node} quadTree2
 * @return {Node}
 */
var intersect = function(quadTree1, quadTree2) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
const intersect = (quadTree1, quadTree2) => {
  if (quadTree1.isLeaf && quadTree2.isLeaf)
    return new Node(quadTree1.val || quadTree2.val, true);
  if (quadTree1.isLeaf)
    return quadTree1.val ? new Node(true, true) : quadTree2;
  if (quadTree2.isLeaf)
    return quadTree2.val ? new Node(true, true) : quadTree1;
  return intersect(quadTree1.topLeft, quadTree2.topLeft).val &&
    intersect(quadTree1.topRight, quadTree2.topRight).val &&
    intersect(quadTree1.bottomLeft, quadTree2.bottomLeft).val &&
    intersect(quadTree1.bottomRight, quadTree2.bottomRight).val ?
    new Node(true, true) :
    new Node(
      quadTree1.val || quadTree2.val,
      false,
      intersect(quadTree1.topLeft, quadTree2.topLeft),
      intersect(quadTree1.topRight, quadTree2.topRight),
      intersect(quadTree1.bottomLeft, quadTree2.bottomLeft),
      intersect(quadTree1.bottomRight, quadTree2.bottomRight),
    );
};
```

## 四 LeetCode Submit



```js
Accepted
* 58/58 cases passed (328 ms)
* Your runtime beats 8.33 % of javascript submissions
* Your memory usage beats 14.29 % of javascript submissions (44 MB)
```

## 五 解题思路



**首先**，先看题目，似懂非懂，那么只有一个法子：

* **以身试法**。

直接提交 Submit 看看它传进来的数据结构是怎样的：

```js
const quadTree1 = {
  "$id": "1",
  "isLeaf": false,
  "val": true,
  "bottomLeft": {
    "$id": "4",
    "isLeaf": true,
    "val": false,
    "bottomLeft": null,
    "bottomRight": null,
    "topLeft": null,
    "topRight": null,
  },
  "bottomRight": {
    "$id": "5",
    "isLeaf": true,
    "val": false,
    "bottomLeft": null,
    "bottomRight": null,
    "topLeft": null,
    "topRight": null,
  },
  "topLeft": {
    "$id": "2",
    "isLeaf": true,
    "val": true,
    "bottomLeft": null,
    "bottomRight": null,
    "topLeft": null,
    "topRight": null,
  },
  "topRight": {
    "$id": "3",
    "isLeaf": true,
    "val": true,
    "bottomLeft": null,
    "bottomRight": null,
    "topLeft": null,
    "topRight": null,
  },
}
const quadTree2 = {
  "$id": "1",
  "isLeaf": false,
  "val": true,
  "bottomLeft": {
    "$id": "8",
    "isLeaf": true,
    "val": true,
    "bottomLeft": null,
    "bottomRight": null,
    "topLeft": null,
    "topRight": null,
  },
  "bottomRight": {
    "$id": "9",
    "isLeaf": true,
    "val": false,
    "bottomLeft": null,
    "bottomRight": null,
    "topLeft": null,
    "topRight": null,
  },
  "topLeft": {
    "$id": "2",
    "isLeaf": true,
    "val": true,
    "bottomLeft": null,
    "bottomRight": null,
    "topLeft": null,
    "topRight": null,
  },
  "topRight": {
    "$id": "3",
    "isLeaf": false,
    "val": true,
    "bottomLeft": {
      "$id": "6",
      "isLeaf": true,
      "val": true,
      "bottomLeft": null,
      "bottomRight": null,
      "topLeft": null,
      "topRight": null,
    },
    "bottomRight": {
      "$id": "7",
      "isLeaf": true,
      "val": true,
      "bottomLeft": null,
      "bottomRight": null,
      "topLeft": null,
      "topRight": null,
    },
    "topLeft": {
      "$id": "4",
      "isLeaf": true,
      "val": false,
      "bottomLeft": null,
      "bottomRight": null,
      "topLeft": null,
      "topRight": null,
    },
    "topRight": {
      "$id": "5",
      "isLeaf": true,
      "val": false,
      "bottomLeft": null,
      "bottomRight": null,
      "topLeft": null,
      "topRight": null,
    },
  },
}
```

OK，明白了，尝试解题：

```js
/**
 * @param {Node} quadTree1
 * @param {Node} quadTree2
 * @return {Node}
 */
const intersect = (quadTree1, quadTree2) => {
  const ergodic = (tree) => {
    if (!tree) {
      return '';
    }
    return '!'
      + tree.val
      + ergodic(tree.bottomLeft)
      + ergodic(tree.bottomRight)
      + ergodic(tree.topLeft)
      + ergodic(tree.topRight);
  };
  console.log(ergodic(quadTree1));
  console.log(ergodic(quadTree2));
};
```

> 注：叶子节点即下面没有更深层次节点的最终节点。

现在，将这两棵树都遍历了：

> node index.js

```
!true!false!false!true!true
!true!true!false!true!true!true!true!false!false
```

那么最重要的来了：**取交集**。

……好吧，突然发现今天时间真的不够，折腾到接近开会才发现还没有完全思路（中间写了工作周报、看了插座学院、跟产品聊了会……）。

查看了下【评论区】，找了份题解：

```js
const intersect = (quadTree1, quadTree2) => {
  if (quadTree1.isLeaf && quadTree2.isLeaf)
    return new Node(quadTree1.val || quadTree2.val, true);
  if (quadTree1.isLeaf)
    return quadTree1.val ? new Node(true, true) : quadTree2;
  if (quadTree2.isLeaf)
    return quadTree2.val ? new Node(true, true) : quadTree1;
  return intersect(quadTree1.topLeft, quadTree2.topLeft).val &&
    intersect(quadTree1.topRight, quadTree2.topRight).val &&
    intersect(quadTree1.bottomLeft, quadTree2.bottomLeft).val &&
    intersect(quadTree1.bottomRight, quadTree2.bottomRight).val ?
    new Node(true, true) :
    new Node(
      quadTree1.val || quadTree2.val,
      false,
      intersect(quadTree1.topLeft, quadTree2.topLeft),
      intersect(quadTree1.topRight, quadTree2.topRight),
      intersect(quadTree1.bottomLeft, quadTree2.bottomLeft),
      intersect(quadTree1.bottomRight, quadTree2.bottomRight),
    );
};
```

Submit 提交后是可行的：

```js
Accepted
* 58/58 cases passed (328 ms)
* Your runtime beats 8.33 % of javascript submissions
* Your memory usage beats 14.29 % of javascript submissions (44 MB)
```

当然，将我们的参数丢上去就不行了，因为 JavaScript 没有 `new Node()` 这种原生操作。

同时，【评论区】仅有 26 条回复，【题解区】仅有 7 条回复，怕不是跑到【困难】题集来了！

经过两天的观看（2019-11-15 08:33:00），只能表示没有正确解释！

如果小伙伴们感兴趣，并且有自己的想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

