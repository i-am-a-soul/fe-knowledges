700 - 二叉搜索树的搜索（search-in-a-binary-search-tree）
===

> Create by **jsliang** on **2019-12-19 08:44:54**  
> Recently revised in **2019-12-19 09:06:07**

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
* **题目地址**：https://leetcode-cn.com/problems/search-in-a-binary-search-tree/
* **题目内容**：

```
给定二叉搜索树（BST）的根节点和一个值。
你需要在 BST 中找到节点值等于给定值的节点。
返回以该节点为根的子树。
如果节点不存在，则返回 NULL。

例如，

给定二叉搜索树:

        4
       / \
      2   7
     / \
    1   3

和值: 2
你应该返回如下子树:

      2     
     / \   
    1   3
在上述示例中，如果要找的值是 5，
但因为没有节点值为 5，我们应该返回 NULL。
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
 * @param {number} val
 * @return {TreeNode}
 */
var searchBST = function(root, val) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 二叉搜索树中的搜索
 * @param {TreeNode} root
 * @param {number} val
 * @return {TreeNode}
 */
const searchBST = (root, val) => {
  if (!root) {
    return null;
  }
  if (root.val > val) {
    return searchBST(root.left, val);
  } else if (root.val < val) {
    return searchBST(root.right, val);
  } else {
    return root;
  }
};

const root = {
  val: 4,
  left: {
    val: 2,
    left: { val: 1, left: null, right: null },
    right: { val: 3, left: null, right: null },
  },
  right: { val: 7, left: null, right: null },
};
console.log(searchBST(root, 2));
// { val: 2,
//   left: { val: 1, left: null, right: null },
//   right: { val: 3, left: null, right: null } }
```

`node index.js` 返回：

```js
{ val: 2,
  left: { val: 1, left: null, right: null },
  right: { val: 3, left: null, right: null } }
```

## 四 LeetCode Submit



```js
Accepted
* 36/36 cases passed (92 ms)
* Your runtime beats 79.06 % of javascript submissions
* Your memory usage beats 21.43 % of javascript submissions (42.1 MB)
```

## 五 解题思路



**做吐了的树，习惯了的数组字符串**。

> 递归

```js
const searchBST = (root, val) => {
  if (!root) {
    return null;
  }
  if (root.val > val) {
    return searchBST(root.left, val);
  } else if (root.val < val) {
    return searchBST(root.right, val);
  } else {
    return root;
  }
};
```

充分利用二叉搜索树的特点，如果：

1. 如果树当前节点大于给定的节点值，那么我们需要往左边递归；
2. 如果树当前节点小于给定的节点值，那么我们需要往右边递归；
3. 如果已经遍历完毕，到最后节点了，那么返回空节点 `null`；
4. 排除 1-3 情况，返回 `root` 即为结果。

enm...感觉说了跟没说一样，纯粹利用搜索二叉树的特点而已。

Submit 提交：

```js
Accepted
* 36/36 cases passed (92 ms)
* Your runtime beats 79.06 % of javascript submissions
* Your memory usage beats 21.43 % of javascript submissions (42.1 MB)
```

吃饱了换个口味，尝试迭代：

> 迭代

```js
const searchBST = (root, val) => {
  const newRoot = [root];
  while (newRoot.length) {
    const tempRoot = newRoot.pop();
    if (!tempRoot) {
      return null;
    } else if (tempRoot.val === val) {
      return tempRoot;
    } else if (tempRoot.val > val) {
      newRoot.push(tempRoot.left);
    } else if (tempRoot.val < val) {
      newRoot.push(tempRoot.right);
    }
  }
};
```

Submit 提交：

```js
Accepted
* 36/36 cases passed (76 ms)
* Your runtime beats 100 % of javascript submissions
* Your memory usage beats 11.9 % of javascript submissions (42.3 MB)
```

决定了，以后要是我搞算法和数据结构的树内容的时候，这道题就是二叉搜索树的典型入门题！

如果小伙伴有更好的思路或者想法，欢迎评论留言或者私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

