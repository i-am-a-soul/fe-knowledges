538 - 把二叉搜索树转换成累加树（convert-bst-to-greater-tree）
===

> Create by **jsliang** on **2019-11-9 19:15:22**  
> Recently revised in **2019-11-9 20:17:43**

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
* **题目地址**：https://leetcode-cn.com/problems/convert-bst-to-greater-tree/
* **题目内容**：

```
给定一个二叉搜索树（Binary Search Tree），把它转换成为累加树（Greater Tree)。

使得每个节点的值是原来的节点值加上所有大于它的节点值之和。

例如：

输入: 二叉搜索树:
    5
  /   \
 2     13

输出: 转换为累加树:
   18
  /   \
20     13
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
 * @return {TreeNode}
 */
var convertBST = function(root) {
  
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 把二叉搜索树转换成累加树
 * @param {TreeNode} root
 * @return {TreeNode}
 */
const convertBST = (root) => {
  const rootList = [];
  const ergodic = (param) => {
    if (!param.root) {
      return;
    }
    // 收集树元素
    if (param.isCollect) {
      rootList.push(param.root.val);
    }
    // 累加树元素
    if (param.isCompute) {
      rootList.filter(item => item > param.root.val).forEach(item => param.root.val += item);
    }
    ergodic({ root: param.root.left, isCompute: param.isCompute, isCollect: param.isCollect });
    ergodic({ root: param.root.right, isCompute: param.isCompute, isCollect: param.isCollect });
  };
  ergodic({
    root,
    isCompute: false, // 非计算模式
    isCollect: true, // 收集模式
  });
  ergodic({
    root,
    isCompute: true, // 计算模式
    isCollect: false, // 非收集模式
  })
  return root;
};

// const root = {
//   val: 5,
//   left: { val: 2, left: null, right: null },
//   right: { val: 13, left: null, right: null },
// };
const root = {
  val: 2,
  left: { val: 1, left: null, right: null },
  right: { val: 3, left: null, right: null },
};

console.log(convertBST(root));
```

`node index.js` 返回：

```js
{ val: 5,
  left: { val: 6, left: null, right: null },
  right: { val: 3, left: null, right: null } }
```

## 四 LeetCode Submit



```js
Accepted
* 212/212 cases passed (632 ms)
* Your runtime beats 5.6 % of javascript submissions
* Your memory usage beats 6.9 % of javascript submissions (50.7 MB)
```

## 五 解题思路



**首先**，日常惯例，周末午觉醒来，一切暴力了事：

```js
/**
 * @name 把二叉搜索树转换成累加树
 * @param {TreeNode} root
 * @return {TreeNode}
 */
const convertBST = (root) => {
  const rootList = [];
  const ergodic = (param) => {
    if (!param.root) {
      return;
    }
    // 收集树元素
    if (param.isCollect) {
      rootList.push(param.root.val);
    }
    // 累加树元素
    if (param.isCompute) {
      rootList.filter(item => item > param.root.val).forEach(item => param.root.val += item);
    }
    ergodic({ root: param.root.left, isCompute: param.isCompute, isCollect: param.isCollect });
    ergodic({ root: param.root.right, isCompute: param.isCompute, isCollect: param.isCollect });
  };
  ergodic({
    root,
    isCompute: false, // 非计算模式
    isCollect: true, // 收集模式
  });
  ergodic({
    root,
    isCompute: true, // 计算模式
    isCollect: false, // 非收集模式
  })
  return root;
};

// const root = {
//   val: 5,
//   left: { val: 2, left: null, right: null },
//   right: { val: 13, left: null, right: null },
// };
const root = {
  val: 2,
  left: { val: 1, left: null, right: null },
  right: { val: 3, left: null, right: null },
};

console.log(convertBST(root));
```

**然后**，得到结果：

```js
Accepted
* 212/212 cases passed (632 ms)
* Your runtime beats 5.6 % of javascript submissions
* Your memory usage beats 6.9 % of javascript submissions (50.7 MB)
```

**最后**，整理下思路：

1. 第一次遍历，是收集模式，即将树的所有元素收集到 `rootList` 中。
2. 第二次遍历，是计算模式，即将树的每个节点，和 `rootList` 中的值进行比较，将它和 `rootList` 中所有比它大的值进行想加。
3. 在 `ergodic` 函数体中，我们使用了 `Object` 的形式进行参数传递，以方便了解参数，虽然还是不怎么好看~

这样，我们就暴力破解了这道题。

## 六 进一步思考



当然，精益求精，一开始我的想法是，能不能直接一次性把所有值搞出来，然后累加，所以我还是求解下【题解】区和【评论】区，看看有没有更好的方法~

> 利用二叉搜索树解题

```js
const convertBST = (root) => {
  let sum = 0;
  const ergodic = (root) => {
    if (!root) {
      return;
    }
    ergodic(root.right);
    sum += root.val;
    root.val = sum;
    ergodic(root.left);
  }
  ergodic(root);
  return root;
};
```

submit 提交：

```js
Accepted
* 212/212 cases passed (104 ms)
* Your runtime beats 84.8 % of javascript submissions
* Your memory usage beats 75.86 % of javascript submissions (39.9 MB)
```

官方题解，最为致命。

这种解法来自官方题解：https://leetcode-cn.com/problems/convert-bst-to-greater-tree/solution/ba-er-cha-sou-suo-shu-zhuan-huan-wei-lei-jia-shu-3/

思想非常秒，是我的忽略：

1. 这是一颗二叉搜索树，所以右子树是大于左子树的，那么我们肯定先走右边！
2. 走完右边后，我们的值就累积起来了，再走左边。

拿题目例子说：

```js
    5
  /   \
 2     13
```

1. 先走到 13，然后 `sum = 13`。
2. 再走到 5，然后 `sum = 18`。
3. 最后走到 2，然后 `sum = 20`。

秒啊~

> 官方题解下面还有迭代和反序中序等方式，如果小伙伴们感兴趣，可以去瞅瞅，或者你有属于自己的想法，欢迎评论留言或者私聊我吐槽~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

