872 - 叶子相似的树（leaf-similar-trees）
===

> Create by **jsliang** on **2020-01-11 10:08:21**  
> Recently revised in **2020-01-11 10:35:53**

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
* **涉及知识**：树、深度优先搜索
* **题目地址**：https://leetcode-cn.com/problems/leaf-similar-trees/
* **题目内容**：

```
请考虑一颗二叉树上所有的叶子，
这些叶子的值按从左到右的顺序排列形成一个 叶值序列 。

     3
    / \
   5   1
 / |   | \
6  2   9  8
  / \
 7   4

举个例子，
如上图所示，
给定一颗叶值序列为 (6, 7, 4, 9, 8) 的树。

如果有两颗二叉树的叶值序列是相同，
那么我们就认为它们是 叶相似 的。

如果给定的两个头结点分别为 root1 和 root2 的树是叶相似的，
则返回 true；否则返回 false 。

提示：

给定的两颗树可能会有 1 到 100 个结点。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root1
 * @param {TreeNode} root2
 * @return {boolean}
 */
var leafSimilar = function(root1, root2) {
    
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
 * @name 叶子相似的树
 * @param {TreeNode} root1
 * @param {TreeNode} root2
 * @return {boolean}
 */
const leafSimilar = (root1, root2) => {
  const ergodic = (root, result = []) => {
    if (!root) {
      return;
    }
    if (!root.left && !root.right) {
      result.push(root.val);
    }
    ergodic(root.left, result);
    ergodic(root.right, result);
    return result;
  }
  const result1 = ergodic(root1);
  const result2 = ergodic(root2);
  return result1.join('') === result2.join('');
};

const root1 = {
  val: 3,
  left: {
    val: 5,
    left: { val: 6, left: null, right: null },
    right: {
      val: 2,
      left: { val: 7, left: null, right: null },
      right: { val: 4, left: null, right: null },
    },
  },
  right: {
    val: 1,
    left: { val: 9, left: null, right: null },
    right: { val: 8, left: null, right: null },
  },
}

const root2 = {
  val: 3,
  left: {
    val: 5,
    left: { val: 6, left: null, right: null },
    right: {
      val: 2,
      left: { val: 7, left: null, right: null },
      right: { val: 4, left: null, right: null },
    },
  },
  right: {
    val: 1,
    left: { val: 9, left: null, right: null },
    right: {
      val: 10,
      left: null,
      right: { val: 8, left: null, right: null },
    },
  },
}

console.log(leafSimilar(root1, root2));
```

`node index.js` 返回：

```js
true
```

## 四 LeetCode Submit



```js
Accepted
* 36/36 cases passed (84 ms)
* Your runtime beats 13.75 % of javascript submissions
* Your memory usage beats 53.57 % of javascript submissions (34.7 MB)
```

## 五 解题思路



**首先**，这道题的题目描述异常不清晰，也不容易理解。

假设两棵树如下所示：

```js
// root1
     3
    / \
   5   1
 / |   | \
6  2   9  8
  / \
 7   4

// root2
     3
    / \
   5   1
 / |   | \
6  2   9  10
  / \       \
 7   4       8
```

这样，它们的 叶值序列 都是：[6, 7 , 4, 9, 8]，是否它们就相似了？咱们代码证明一下~

**然后**，在这之前，相信这么久没看到树的题目，小伙伴应该忘记树的万能公式了，咱们过过：

> 树的万能公式

```js
const root = {
  val: 2,
  left: { val: 1, left: null, right: null },
  right: { val: 3, left: null, right: null },
}
const ergodic = (root) => {
  if (!root) {
    return '!#';
  }
  return '!' + root.val + ergodic(root.left) + ergodic(root.right);
}
console.log(ergodic(root));
// !2!1!#!#!3!#!#
```

OK，那么如何获取两棵树的根节点也就顺势而生了：

> 递归

```js
const leafSimilar = (root1, root2) => {
  const ergodic = (root, result = []) => {
    if (!root) {
      return;
    }
    if (!root.left && !root.right) {
      result.push(root.val);
    }
    ergodic(root.left, result);
    ergodic(root.right, result);
    return result;
  }
  const result1 = ergodic(root1);
  const result2 = ergodic(root2);
  return result1.join('') === result2.join('');
};
```

**最后**，Submit 提交：

```js
Accepted
* 36/36 cases passed (84 ms)
* Your runtime beats 13.75 % of javascript submissions
* Your memory usage beats 53.57 % of javascript submissions (34.7 MB)
```

成功破解！

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

