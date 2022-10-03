104 - 二叉树的最大深度（maximum-depth-of-binary-tree）
===

> Create by **jsliang** on **2019-06-14 16:18:02**  
> Recently revised in **2019-06-14 17:15:44**

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
| [七 进一步思考](#chapter-seven) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：树
* **题目地址**：深度优先搜索
* **题目内容**：

```
给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

示例：
给定二叉树 [3,9,20,null,null,15,7]，

    3
   / \
  9  20
    /  \
   15   7

返回它的最大深度 3 。
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var maxDepth = function(root) {
  if (!root) {
    return 0;
  }
  let longest = 1;
  let ergodic = function(root, depth) {
    if (!root) {
      return;
    }
    if (root.left || root.right) {
      depth += 1;
      if (depth > longest) {
        longest = depth;
      }
      ergodic(root.left, depth);
      ergodic(root.right, depth);
    }
  }
  ergodic(root, 1);
  return longest;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



* 参数 `root`：

```js
let root = {
  val: 3,
  left: { val: 9, left: null, right: null, },
  right: {
    val: 20,
    left: { val: 15, left: null, right: null },
    right: { val: 7, left: null, right: null },
  },
}
```

* 返回值 `return`：

```js
3
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
✔ Accepted
  ✔ 39/39 cases passed (92 ms)
  ✔ Your runtime beats 91.94 % of javascript submissions
  ✔ Your memory usage beats 12.78 % of javascript submissions (37.4 MB)
```

## <a name="chapter-six" id="chapter-six">六 解题思路</a>



**首先**，如果小伙伴们还记得我们的万能公式：

```js
let traverse = function(root) {
  // root 需要做什么？在这做。
  // 其他的不用 root 操心，抛给框架
  traverse(root.left);
  traverse(root.right);
}
```

那么你或许已经有思路了。

**然后**，为了方便从没接触过树解法的小伙伴们，**jsliang** 将这道题解题思路从头讲讲：

* 步骤 1：判断非空。如果是空的直接返回 0。

```js
if (!root) {
  return 0;
}
```

* 步骤 2：由于前面判断非空了，所以现在最长的深度是 `1`，我们从 `1` 继续。

```js
let longest = 1;
```

* 步骤 3：基于破解二叉树套路，开始解题。

```js
let ergodic = function(root, depth) {
  if (!root) {
    return;
  }
  if (root.left || root.right) {
    depth += 1;
    if (depth > longest) {
      longest = depth;
    }
    ergodic(root.left, depth);
    ergodic(root.right, depth);
  }
}
ergodic(root, 1);
```

在这里，我们判断 `root` 是否还存在 `left` 和 `right`：如果不存在，那么树到了最底层，终止递归；如果存在，那么 `depth` 深度 `+ 1`，并且遍历它的左树和右树。

同时，我们在树存在 `left` 和 `right` 的时候，将 `depth` 和 `longest` 比较，把最深的树给记录下来。

* 步骤 4：返回最长深度 `longest`。

**最后**，我们就完成了这道求树最大深度的破解，小伙伴们是不是感觉思路一下子打开了？

那么，我们继续看下去。

## <a name="chapter-seven" id="chapter-seven">七 进一步思考</a>



**jsiang** 破解完这道题后，逛了下这道题的【题解】和【评论】，看到了一个优秀的代码，深感惭愧：

```js
var maxDepth = function(root) {
  if(!root) return 0;
  return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
};
```

震惊有木有，哈哈，直接两行代码搞定！

但是，这还不是最佳的：

```js
var maxDepth = function(root) {
  return root === null ? 0 : Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
};
```

好的吧，一行代码搞定了……面壁去！哈哈

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

