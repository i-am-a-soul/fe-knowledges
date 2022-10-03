110 - 平衡二叉树（balanced-binary-tree）
===

> Create by **jsliang** on **2019-6-24 07:48:53**  
> Recently revised in **2019-09-18 10:23:56**

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
| [七 进一步思考](#chapter-seven) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：树、深度优先搜索
* **题目地址**：https://leetcode-cn.com/problems/balanced-binary-tree/
* **题目内容**：

```
给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。

示例 1:
给定二叉树 [3,9,20,null,null,15,7]

    3
   / \
  9  20
    /  \
   15   7
返回 true 。

示例 2:
给定二叉树 [1,2,2,3,3,null,null,4,4]

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
返回 false 。
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var isBalanced = function(root) {
  let ergodic = function(root) {
    if (!root) {
      return 0;
    }
    let left = ergodic(root.left);
    if (left === -1) {
      return -1;
    }
    let right = ergodic(root.right);
    if (right === -1) {
      return -1;
    }
    return Math.abs(left - right) < 2 ? Math.max(left, right) + 1 : -1;
  }
  return ergodic(root) !== -1;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



* `root`：

```js
//   3
//  / \
// 9  20
//   /  \
//  15   7
let root = {
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
true
```

* **LeetCode Submit**：

```js
√ Accepted
  √ 227/227 cases passed (88 ms)
  √ Your runtime beats 98.58 % of javascript submissions
  √ Your memory usage beats 31.68 % of javascript submissions (37.7 MB)
```

## <a name="chapter-five" id="chapter-five">五 知识点</a>



`Math`：JS 中的内置对象，具有数学常数和函数的属性和方法。[`Math` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Math/README.md)

## <a name="chapter-six" id="chapter-six">六 解题思路</a>



**首先**，我们需要明白题意，怎样的树不符合平衡二叉树呢？

> 案例 1

```js
  3
 / \
9  20
     \
      7
       \
        2
```

> 案例 2

```js
  3
 / \
9  20
  /  \
 3    7
       \
        2
```

**然后**，我们查看下它遍历情况，它为什么不符合我们的要求了？

> 以案例 2 为参考

```js
let root = {
  val: 3,
  left: { val: 9, left: null, right: null },
  right: {
    val: 20,
    left: { val: 3, left: null, right: null },
    right: {
      val: 7,
      left: null,
      right: { val: 2, left: null, right: null },
    },
  },
}

var isBalanced = function(root) {
  let ergodic = function(root) {
    if (!root) {
      return 0;
    }
    let left = ergodic(root.left);
    if (left === -1) {
      return -1;
    }
    let right = ergodic(root.right);
    if (right === -1) {
      return -1;
    }
    console.log('------');
    console.log(left, right);
    console.log(root);
    return Math.abs(left - right) < 2 ? Math.max(left, right) + 1 : -1;
  }
  return ergodic(root) != -1;
};

console.log(isBalanced(root));
```

小伙伴们可以猜测下打印结果：

```js
------
0 0
{ val: 9, left: null, right: null }
------
0 0
{ val: 3, left: null, right: null }
------
0 0
{ val: 2, left: null, right: null }
------
0 1
{ val: 7,
  left: null,
  right: { val: 2, left: null, right: null } }
------
1 2
{ val: 20,
  left: { val: 3, left: null, right: null },
  right:
   { val: 7,
     left: null,
     right: { val: 2, left: null, right: null } } }
------
1 3
{ val: 3,
  left: { val: 9, left: null, right: null },
  right:
   { val: 20,
     left: { val: 3, left: null, right: null },
     right: { val: 7, left: null, right: [Object] } } }
false
```

在这里，由于我们是以递归的形式，所以，我们会先遍历左节点，再遍历右节点，最后再遍历根节点（后序遍历）

同时，我们判断左右树的高度差是否超过 `1`，如果是，则进行中断，返回 `false`；否则，继续递归。

**最后**，我们将遍历的结果与 `-1` 进行比较，返回 `true` 或者 `false`

## <a name="chapter-seven" id="chapter-seven">七 进一步思考</a>



这里给基础教弱的同学补个知识点：**递归**

我们结合题意来讲，假设我们有一个对象：

```js
const obj = {
  val: 1,
  next: {
    val: 2,
    next: {
      val: 3,
      next: {
        val: null,
      }
    }
  }
}

// 1 -> 2 -> 3 -> null
```

我们需要遍历这个链表的所有节点，我们会怎么做呢？

```js
let regodic = function(obj) {
  if (!obj.next) return '!#';
  return '!' + obj.val + regodic(obj.next);
}
console.log(regodic(obj));
```

那么它会输出什么呢？

答案是：`!1!2!3!#`

是的，最底层返回 `!#`

然后递归上一层，变成 `!3!#`

再上一层，变成 `!2!3!#`

再再上一层，得到最终答案，变成 `!1!2!3!#`

那么，讲到这里，小伙伴们再回顾这道题，应该知道为什么 `left` 和 `right` 的值会按照我们想法行事的了。

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

