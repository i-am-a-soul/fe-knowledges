111 - 二叉树的最小深度（minimum-depth-of-binary-tree）
===

> Create by **jsliang** on **2019-6-25 07:46:07**  
> Recently revised in **2019-09-18 10:24:32**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| [四 执行测试](#chapter-four) |
| [五 知识点](#chapter-five) |
| [六 解题思路](#chapter-six) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：树、深度优先搜索、广度优先搜索
* **题目地址**：https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/
* **题目内容**：

```
给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

说明: 叶子节点是指没有子节点的节点。

示例:

给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回它的最小深度  2.
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var minDepth = function(root) {
  if (!root) {
    return 0;
  }
  if (!root.left) {
    return minDepth(root.right) + 1;
  }
  if (!root.right) {
    return minDepth(root.left) + 1;
  }
  return Math.min(minDepth(root.left), minDepth(root.right)) + 1;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



* `root`：

```js
const root = {
  val: 3,
  left: { val: 9, left: null, right: null },
  right: {
    val: 20,
    left: { val: 15, left: null, right: null },
    right: { val: 7, left: null, right: null },
  },
}
```

* `return`：

```js
2
```

* **LeetCode Submit**：

```js
√ Accepted
  √ 41/41 cases passed (80 ms)
  √ Your runtime beats 98.52 % of javascript submissions
  √ Your memory usage beats 8.64 % of javascript submissions (37.7 MB)
```

## <a name="chapter-five" id="chapter-five">五 知识点</a>



`Math`：JS 中的内置对象，具有数学常数和函数的属性和方法。[`Math` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Math/README.md)

## <a name="chapter-six" id="chapter-six">六 解题思路</a>



说说 **jsliang** 的思路：

假设我是一只蜘蛛，我在一颗大树最底下（根节点），开始往上爬。

每经过 1 米（1 个 val 节点），我就留下一个分身。

当我爬到最顶的时候，我就进行最后标记，并告诉分身，前面凉凉了，开始报数！

于是从我为 1 开始，一直到根节点的长度，就是这个分支的高度。

消掉这条分支后，继续其他分支……

```js

// root：
//   3
//  / \
// 9  20
//   /  \
//  15   7
const root = {
  val: 3,
  left: { val: 9, left: null, right: null },
  right: {
    val: 20,
    left: { val: 15, left: null, right: null },
    right: { val: 7, left: null, right: null },
  },
}
var minDepth = function(root) {
  if (!root) {
    return 0;
  }
  if (!root.left) {
    return minDepth(root.right) + 1;
  }
  if (!root.right) {
    return minDepth(root.left) + 1;
  }
  return Math.min(minDepth(root.left), minDepth(root.right)) + 1;
};
minDepth(root);
```

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

