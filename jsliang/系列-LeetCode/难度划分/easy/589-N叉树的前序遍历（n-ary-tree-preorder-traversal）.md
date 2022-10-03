589 - N叉树的前序遍历（n-ary-tree-preorder-traversal）
===

> Create by **jsliang** on **2019-11-22 08:47:39**  
> Recently revised in **2019-11-22 09:27:43**

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
* **题目地址**：https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/
* **题目内容**：

```
给定一个 N 叉树，返回其节点值的前序遍历。

例如，给定一个 3叉树 :

          1
      /   |   \
    3     2     4
  /  \
 5    6

返回其前序遍历: [1,3,5,6,2,4]。

说明: 递归法很简单，你可以使用迭代法完成此题吗?
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * // Definition for a Node.
 * function Node(val, children) {
 *    this.val = val;
 *    this.children = children;
 * };
 */
/**
 * @param {Node} root
 * @return {number[]}
 */
var preorder = function(root) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * // Definition for a Node.
 * function Node(val, children) {
 *    this.val = val;
 *    this.children = children;
 * };
 */
/**
 * @name N叉树的前序遍历
 * @param {Node} root
 * @param {}
 * @return {number[]}
 */
const preorder = (root) => {
  const result = [];
  const ergodic = (root) => {
    if (!root) {
      return;
    }
    result.push(root.val);
    root.children && root.children.forEach(item => ergodic(item));
  };
  ergodic(root);
  return result;
};

const root = {
  val: 1,
  children: [
    {
      val: 3,
      children: [
        { val: 5, children: null },
        { val: 6, children: null },
      ],
    },
    { val: 2, children: null },
    { val: 4, children: null },
  ],
};

console.log(preorder(root));
```

`node index.js` 返回：

```js
[1, 3, 5, 6, 2, 4]
```

## 四 LeetCode Submit



```js
Accepted
* 37/37 cases passed (80 ms)
* Your runtime beats 100 % of javascript submissions
* Your memory usage beats 100 % of javascript submissions (37.3 MB)
```

## 五 解题思路



**你知道我在想什么，如果你看过我之前破解树的题目……**

直接万能公式递归暴力破解啦：

```js
const preorder = (root) => {
  const result = [];
  const ergodic = (root) => {
    if (!root) {
      return;
    }
    result.push(root.val);
    root.children && root.children.forEach(item => ergodic(item));
  };
  ergodic(root);
  return result;
};
```

Submit 提交：

```js
Accepted
* 37/37 cases passed (80 ms)
* Your runtime beats 100 % of javascript submissions
* Your memory usage beats 100 % of javascript submissions (37.3 MB)
```

哇喔，一百婚，妈妈我终于又拿到语文英语一百分了~

那么本题就此结束……啪，咱要精益求精！

## 六 进一步思考



在题目中，有句话：

* 说明: 递归法很简单，你可以使用迭代法完成此题吗?

哦豁？**jsliang** 能说自己不会迭代吗？

```js
const preorder = (root) => {
  if (!root) {
    return [];
  }
  const result = [], tempRoot = [root];
  while (tempRoot.length) {
    const current = tempRoot.pop();
    result.push(current.val);
    if (current.children) {
      for (let i = current.children.length - 1; i >= 0; i--) {
        tempRoot.push(current.children[i]);
      }
    }
  }
  return result;
};
```

Submit 提交：

```js
Accepted
* 37/37 cases passed (92 ms)
* Your runtime beats 97.84 % of javascript submissions
* Your memory usage beats 100 % of javascript submissions (37.6 MB)
```

攻略如下：

1. 如果传进来的是空树，则返回 `[]`。
2. 将 `tempRoot` 看做是每一个子树（初始化的时候将整棵树当成子树）。
3. 遍历 `tempRoot`，只要它还有长度（意味着我们需要遍历所有项）。
4. 设置 `current` 为当前树（`tempRoot`）的末尾项，逐项遍历，判断其是否有 `children`，如果有，那么说明还可以进一步查找。
5. 循环 `current.children`，将其添加进 `tempRoot` 中。直到 `tempRoot` 的项都被推出来，表明内部不在存在项。
6. 循环结束，返回 `result`。

这样，这道题的破解就此结束，如果小伙伴们有更好的思路或者想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

