501 - 二叉搜索树中的众数（find-mode-in-binary-search-tree）
===

> Create by **jsliang** on **2019-10-31 19:00:37**  
> Recently revised in **2019-10-31 19:30:55**

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
* **题目地址**：https://leetcode-cn.com/problems/find-mode-in-binary-search-tree/
* **题目内容**：

```
给定一个有相同值的二叉搜索树（BST），找出 BST 中的所有众数

> 众数：出现频率最高的元素。

假定 BST 有如下定义：

结点左子树中所含结点的值小于等于当前结点的值
结点右子树中所含结点的值大于等于当前结点的值
左子树和右子树都是二叉搜索树

例如：
给定 BST [1,null,2,2],

   1
    \
     2
    /
   2
返回[2].

提示：如果众数超过1个，不需考虑输出顺序

进阶：你可以不使用额外的空间吗？

> 假设由递归产生的隐式调用栈的开销不被计算在内
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var findMode = function(root) {
  
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 二叉搜索树中的众数
 * @param {TreeNode} root
 * @return {number[]}
 */
const findMode = (root) => {
  let result = [];
  let map = new Map();
  let max = 0;
  const regodic = (root) => {
    if (!root) {
      return '!#'
    }
    if (map.get(root.val) === undefined) {
      map.set(root.val, 1);
    } else {
      map.set(root.val, map.get(root.val) + 1);
    }
    max = Math.max(max, map.get(root.val));
    return `!${root.val}${regodic(root.left)}${regodic(root.right)}`;
  }
  regodic(root);
  for (let [key, value] of map.entries()) {
    if (value === max) {
      result.push(key);
    }
  }
  return result;
};

const root = {
  val: 1,
  left: null,
  right: {
    val: 2,
    left: {
      val: 2,
      left: null,
      right: null,
    },
    right: null,
  }
};
console.log(findMode(root));
```

`node index.js` 返回：

```js
[2]
```

## 四 LeetCode Submit



```js
Accepted
* 25/25 cases passed (92 ms)
* Your runtime beats 76.47 % of javascript submissions
* Your memory usage beats 7.69 % of javascript submissions (44 MB)
```

## 五 解题思路



**首先**，说到树，第一时间我又想起了我的万能公式，试了下还没忘：

```js
const regodic = (root) => {
  if (!root) {
    return '!#'
  }
  return `!${root.val}${regodic(root.left)}${regodic(root.right)}`;
}
regodic(root);
// 举例上面的树
// !1!#!2!2!#!#!#
```

**然后**，尝试解决问题：

```js
/**
 * @name 二叉搜索树中的众数
 * @param {TreeNode} root
 * @return {number[]}
 */
const findMode = (root) => {
  let result = [];
  let map = new Map();
  let max = 0;
  const regodic = (root) => {
    if (!root) {
      return '!#'
    }
    if (map.get(root.val) === undefined) {
      map.set(root.val, 1);
    } else {
      map.set(root.val, map.get(root.val) + 1);
    }
    max = Math.max(max, map.get(root.val));
    return `!${root.val}${regodic(root.left)}${regodic(root.right)}`;
  }
  regodic(root);
  for (let [key, value] of map.entries()) {
    if (value === max) {
      result.push(key);
    }
  }
  return result;
};
```

Submit 提交试试：

```js
Accepted
* 25/25 cases passed (92 ms)
* Your runtime beats 76.47 % of javascript submissions
* Your memory usage beats 7.69 % of javascript submissions (44 MB)
```

好，完事，跑路~

> 感兴趣的小伙伴可以做下进阶，**jsliang** 这边还未下班先不搞了

有更好的答案的小伙伴可以留言评论或者私聊哈~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

