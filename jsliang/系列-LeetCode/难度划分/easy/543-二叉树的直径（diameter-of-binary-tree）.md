543 - 二叉树的直径（diameter-of-binary-tree）
===

> Create by **jsliang** on **2019-11-11 08:40:04**  
> Recently revised in **2019-11-11 09:24:36**

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
* **题目地址**：https://leetcode-cn.com/problems/diameter-of-binary-tree/
* **题目内容**：

```
给定一棵二叉树，你需要计算它的直径长度。

一棵二叉树的直径长度是任意两个结点路径长度中的最大值。

这条路径可能穿过根结点。

示例 :
给定二叉树

          1
         / \
        2   3
       / \     
      4   5    
返回 3, 它的长度是路径 [4,2,1,3] 或者 [5,2,1,3]。

注意：两结点之间的路径长度是以它们之间边的数目表示。
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
 * @param {TreeNode} root
 * @return {number}
 */
var diameterOfBinaryTree = function(root) {
  
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
 * @name 二叉树的直径
 * @param {TreeNode} root
 * @return {number}
 */
const diameterOfBinaryTree = (root) => {
  let deep = 0;
  const ergodic = (root) => {
    if (!root) {
      return 0;
    }
    const leftDepth = ergodic(root.left);
    const rightDepth = ergodic(root.right);
    deep = Math.max(deep, leftDepth + rightDepth);
    return Math.max(leftDepth, rightDepth) + 1;
  };
  ergodic(root);
  return deep;
};

const root = {
  val: 1,
  left: {
    val: 2,
    left: { val: 4, left: null, right: null },
    right: { val: 5, left: null, right: null },
  },
  right: { val: 3, left: null, right: null },
}
console.log(diameterOfBinaryTree(root)); // 3
```

`node index.js` 返回：

```js
3
```

## 四 LeetCode Submit



```js
Accepted
* 106/106 cases passed (68 ms)
* Your runtime beats 97.19 % of javascript submissions
* Your memory usage beats 55 % of javascript submissions (37.1 MB)
```

## 五 解题思路



**首先**，看完题目，盖棺定论：

* 该树的最大直径等于左子树的最大深度 + 右子树的最大深度。

定义完毕，直接躺尸试试：

```js
const diameterOfBinaryTree = (root) => {
  let deep = 0;
  const ergodic = (root) => {
    if (!root) {
      return 0;
    }
    const leftDepth = ergodic(root.left);
    const rightDepth = ergodic(root.right);
    deep = Math.max(deep, leftDepth + rightDepth);
    return Math.max(leftDepth, rightDepth) + 1;
  };
  ergodic(root);
  return deep;
};

const root = {
  val: 1,
  left: {
    val: 2,
    left: { val: 4, left: null, right: null },
    right: { val: 5, left: null, right: null },
  },
  right: { val: 3, left: null, right: null },
}

console.log(diameterOfBinaryTree(root)); // 3
```

Submit 提交结果：

```js
Accepted
* 106/106 cases passed (68 ms)
* Your runtime beats 97.19 % of javascript submissions
* Your memory usage beats 55 % of javascript submissions (37.1 MB)
```

满足~

下面说说解法：

1. 定义深度 `deep`。
2. 求出左子树的最大深度和右子树的最大深度
3. `deep` 记录当前的最大直径
4. `return` 左子树或者右子树的最大深度 + 1

这样，我们就完成了这道题的破解啦！

如果小伙伴们有更好的方式，可以评论留言或者直接私聊我~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

