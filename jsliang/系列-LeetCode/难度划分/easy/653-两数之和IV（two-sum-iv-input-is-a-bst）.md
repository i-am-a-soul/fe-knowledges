653 - 两数之和IV（two-sum-iv-input-is-a-bst）
===

> Create by **jsliang** on **2019-12-05 08:39:41**  
> Recently revised in **2019-12-05 09:37:03**

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
* **涉及知识**：树
* **题目地址**：https://leetcode-cn.com/problems/two-sum-iv-input-is-a-bst/
* **题目内容**：

```
给定一个二叉搜索树和一个目标结果，
如果 BST （二叉搜索树）中存在两个元素且它们的和等于给定的目标结果，
则返回 true。

案例 1:

输入: 
    5
   / \
  3   6
 / \   \
2   4   7

Target = 9

输出: True
 

案例 2:

输入: 
    5
   / \
  3   6
 / \   \
2   4   7

Target = 28

输出: False
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
 * @param {number} k
 * @return {boolean}
 */
var findTarget = function(root, k) {
    
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
 * @name 两数之和IV-输入BST
 * @param {TreeNode} root
 * @param {number} k
 * @return {boolean}
 */
const findTarget = (root, k) => {
  const map = new Map();
  let result = false;
  const ergodic = (root) => {
    if (!root) {
      return;
    }
    if (map.get(root.val) !== undefined) {
      result = true;
      return;
    }
    map.set(k - root.val, root.val);
    ergodic(root.left);
    ergodic(root.right);
  };
  ergodic(root);
  return result;
};

const root = {
  val: 5,
  left: {
    val: 3,
    left: { val: 2, left: null, right: null },
    right: { val: 4, left: null, right: null },
  },
  right: {
    val: 6,
    left: null,
    right: { val: 7, left: null, right: null },
  },
};
const target = 9;
// true

console.log(findTarget(root, target));
```

`node index.js` 返回：

```js
true
```

## 四 LeetCode Submit



```js
Accepted
* 421/421 cases passed (104 ms)
* Your runtime beats 66.36 % of javascript submissions
* Your memory usage beats 91.18 % of javascript submissions (41.1 MB)
```

## 五 解题思路



**这道题简单来说是送分题**。

**首先**，咱们不管它是不是二叉搜索树，咱们需要做的，是遍历一遍这棵树：

```js
const findTarget = (root, k) => {
  const ergodic = (root) => {
    if (!root) {
      return;
    }
    ergodic(root.left);
    ergodic(root.right);
  };
  ergodic(root);
};
console.log(findTarget(root, k));
```

**然后**，咱们回想下，怎么求两数之和？

我们是不是可以定义一个哈希表 `Map`，然后每次遍历一个数字，我们就记录 `k - num` 的值，这样下次碰到出现了 `k - num` 的值，我们就结束递归，返回结果即可：

> 递归破解

```js
const findTarget = (root, k) => {
  const map = new Map();
  let result = false;
  const ergodic = (root) => {
    if (!root) {
      return;
    }
    if (map.get(root.val) !== undefined) {
      result = true;
      return;
    }
    map.set(k - root.val, root.val);
    ergodic(root.left);
    ergodic(root.right);
  };
  ergodic(root);
  return result;
};
```

Submit 提交：

```js
Accepted
* 421/421 cases passed (104 ms)
* Your runtime beats 66.36 % of javascript submissions
* Your memory usage beats 91.18 % of javascript submissions (41.1 MB)
```

**最后**，箭头函数中套用了箭头函数，看起来就感觉怪怪的，咱们改造下原方法，进一步优化：

> 优化递归破解

```js
const findTarget = (root, k, map = new Map()) => {
  if (!root) {
    return false;
  }
  if (map.get(root.val) !== undefined) {
    return true;
  }
  map.set(k - root.val, root.val);
  return findTarget(root.left, k, map) || findTarget(root.right, k, map);
};
```

Submit 提交：

```js
Accepted
* 421/421 cases passed (92 ms)
* Your runtime beats 91.59 % of javascript submissions
* Your memory usage beats 55.88 % of javascript submissions (41.8 MB)
```

舒服多了！

**最后的最后**，既然递归搞完了，那么试试迭代吧~

> 迭代破解

```js
const findTarget = (root, k) => {
  const tree = [root];
  const treeList = [];
  let result = false;
  while(tree.length) {
    const tempRoot = tree.pop();
    if (treeList.includes(tempRoot.val)) {
      result = true;
      break;
    }
    treeList.push(k - tempRoot.val);
    if (tempRoot.left) {
      tree.push(tempRoot.left);
    }
    if (tempRoot.right) {
      tree.push(tempRoot.right);
    }
  }
  return result;
};
```

Submit 提交：

```js
Accepted
* 421/421 cases passed (164 ms)
* Your runtime beats 16.82 % of javascript submissions
* Your memory usage beats 26.47 % of javascript submissions (42.1 MB)
```

OK，成功搞定~

> 不得不佩服我自己，哈哈~

## 六 进一步思考



**那么**，肯定还有优化点，例如：

* BST

是的，我们没有利用题目给出的树的类型啦，如果利用 BST 的结构做事，肯定好很多。

如果小伙伴们有其他思路或者如何利用 BST 的，欢迎评论留言或者私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

