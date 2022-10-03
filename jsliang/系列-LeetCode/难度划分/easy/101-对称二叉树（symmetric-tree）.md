101 - 对称二叉树（symmetric-tree）
===

> Create by **jsliang** on **2019-6-14 08:21:33**  
> Recently revised in **2019-6-14 08:56:26**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| [四 执行测试](#chapter-four) |
| [五 LeetCode Submit](#chapter-five) |
| [六 解题思路](#chapter-six) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：树、深度优先搜索、广度优先搜索
* **题目地址**：https://leetcode-cn.com/problems/symmetric-tree/
* **题目内容**：

```
给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

    1
   / \
  2   2
 / \ / \
3  4 4  3

但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

    1
   / \
  2   2
   \   \
   3    3

说明:
如果你可以运用递归和迭代两种方法解决这个问题，会很加分。
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var isSymmetric = function(root) {
  if (!root) {
    return true;
  }
  const leftTree = root.left;
  const rightTree = root.right;
  // 思路，将左侧树或者右侧数反过来遍历
  let leftErgodic = function(root) {
    if (!root) {
      return '!#'
    }
    return `${root.val}!${leftErgodic(root.left)}${leftErgodic(root.right)}`;
  }
  let rightErgodic = function(root) {
    if (!root) {
      return '!#'
    }
    return `${root.val}!${rightErgodic(root.right)}${rightErgodic(root.left)}`;
  }
  return leftErgodic(leftTree) === rightErgodic(rightTree);
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



* 变量 `root`：

```js
let root = {
  val: 1,
  left: {
    val: 2,
    left: { val: 3, left: null, right: null, },
    right: { val: 4, left: null, right: null, },
  },
  right: {
    val: 2,
    left: { val: 4, left: null, right: null, },
    right: { val: 3, left: null, right: null, }
  },
}
```

* 返回值 `return`：

```js
true
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
√ Accepted
  √ 195/195 cases passed (88 ms)
  √ Your runtime beats 92.04 % of javascript submissions
  √ Your memory usage beats 5.15 % of javascript submissions (37 MB)
```

## <a name="chapter-six" id="chapter-six">六 解题思路</a>



**首先**，如果小伙伴有看过上一篇 [100-相同的树（same-tree）](https://github.com/LiangJunrong/document-library/blob/master/other-library/LeetCode/easy/100-%E7%9B%B8%E5%90%8C%E7%9A%84%E6%A0%91%EF%BC%88same-tree%EF%BC%89.md) 的攻略，应该知道破解树的算法有一个套路：

```js
let traverse = function(root) {
  // root 需要做什么？在这做。
  // 其他的不用 root 操心，抛给框架
  traverse(root.left);
  traverse(root.right);
}
```

所以，在这里，我们需要做的，就是将除第一个节点外，它的左侧树和右侧树遍历出来。

**然后**，因为我们需要的是这个数是否是镜像二叉树（对称二叉树），那么我们就应该将左侧树从左到右遍历，将右侧数从右到左遍历，这样它们的顺序就会一致：

```js
const leftTree = root.left;
const rightTree = root.right;
let leftErgodic = function(root) {
  if (!root) {
    return '!#'
  }
  return `${root.val}!${leftErgodic(root.left)}${leftErgodic(root.right)}`;
}
let rightErgodic = function(root) {
  if (!root) {
    return '!#'
  }
  return `${root.val}!${rightErgodic(root.right)}${rightErgodic(root.left)}`;
}
```

这样，我们就会得到两个字符串：

```js
2!3!!#!#4!!#!#
2!3!!#!#4!!#!#
```

**最后**，我们返回它们的比较即可。

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

