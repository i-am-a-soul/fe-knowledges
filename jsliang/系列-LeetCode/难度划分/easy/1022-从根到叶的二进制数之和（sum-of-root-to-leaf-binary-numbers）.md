1022 - 从根到叶的二进制数之和（sum-of-root-to-leaf-binary-numbers）
===

> Create by **jsliang** on **2020-01-29 23:32:01**  
> Recently revised in **2020-01-29 23:59:27**

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
* **题目地址**：https://leetcode-cn.com/problems/sum-of-root-to-leaf-binary-numbers/
* **题目内容**：

```
给出一棵二叉树，
其上每个结点的值都是 0 或 1 。

每一条从根到叶的路径都代表一个从最高有效位开始的二进制数。

例如，如果路径为 0 -> 1 -> 1 -> 0 -> 1，
那么它表示二进制数 01101，也就是 13 。

对树上的每一片叶子，
我们都要找出从根到该叶子的路径所表示的数字。

以 10^9 + 7 为模，
返回这些数字之和。

示例：

     1
   /   \
  0     1
 / \   / \
0   1 0   1

输入：[1,0,1,0,1,0,1]
输出：22
解释：(100) + (101) + (110) + (111) = 4 + 5 + 6 + 7 = 22
 
提示：

树中的结点数介于 1 和 1000 之间。
node.val 为 0 或 1 。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/sum-of-root-to-leaf-binary-numbers
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
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
var sumRootToLeaf = function(root) {
    
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
 * @name 从根到叶的二进制数之和
 * @param {TreeNode} root
 * @return {number}
 */
const sumRootToLeaf = (root) => {
  let result = 0;
  const ergodic = (root, temp) => {
    if (!root) {
      return;
    }
    temp += root.val;
    if (!root.left && !root.right) {
      result += parseInt(temp, 2);
    }
    ergodic(root.left, temp);
    ergodic(root.right, temp);
  };
  ergodic(root, '');
  return result;
};

const root = {
  val: 1,
  left: {
    val: 0,
    left: { val: 0, left: null, right: null },
    right: { val: 1, left: null, right: null },
  },
  right: {
    val: 1,
    left: { val: 0, left: null, right: null },
    right: { val: 1, left: null, right: null },
  },
};

console.log(sumRootToLeaf(root)); // 22
```

`node index.js` 返回：

```js
22
```

## 四 LeetCode Submit



```js
Accepted
* 63/63 cases passed (76 ms)
* Your runtime beats 55.38 % of javascript submissions
* Your memory usage beats 21.05 % of javascript submissions (36.1 MB)
```

## 五 解题思路



记得前面就讲过【树】和【二进制和十进制相互转换】这两个点，但是总有小伙伴可能遗漏，所以咱们回顾下：

> 树的万能公式

```js
const ergodic = (root) => {
  if (!root) {
    return;
  }
  ergodic(root.left);
  ergodic(root.right);
};
ergodic(root);
```

那么，如何获取每条树的分支呢？

如果你喜欢折腾，那么可以发现：

> 获取每条树的分支

```js
const ergodic = (root, temp) => {
  if (!root) {
    return;
  }
  temp += root.val;
  if (!root.left && !root.right) {
    console.log(temp);
  }
  ergodic(root.left, temp);
  ergodic(root.right, temp);
};
ergodic(root, '');
```

我们往递归函数中添加 `temp` 参数，该参数默认为 `''`，这样，当我们每次碰到节点的时候，我们就往当中添加节点。

直到我们碰到这个节点没有 `left` 和 `right` 节点为止，我们就判断它到了这棵树的叶子节点。

再来，我们知道 JavaScript 有个原生方法 `parseInt(num, 2)`，可以将 10 进制转换成 2 进制，所以我们不妨：

> 递归破解

```js
const sumRootToLeaf = (root) => {
  let result = 0;
  const ergodic = (root, temp) => {
    if (!root) {
      return;
    }
    temp += root.val;
    if (!root.left && !root.right) {
      result += parseInt(temp, 2);
    }
    ergodic(root.left, temp);
    ergodic(root.right, temp);
  };
  ergodic(root, '');
  return result;
};
```

OK，不是什么大难事，搞定完事~

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

