100 - 相同的树（same-tree）
===

> Create by **jsliang** on **2019-6-13 07:36:52**  
> Recently revised in **2019-6-13 08:56:03**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题 - 二叉树](#chapter-three) |
| [四 执行测试](#chapter-four) |
| [五 LeetCode Submit](#chapter-five) |
| [六 解题思路](#chapter-six) |
| [七 进一步思考](#chapter-seven) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：树、深度优先搜索
* **题目地址**：https://leetcode-cn.com/problems/same-tree/
* **题目内容**：

```
给定两个二叉树，编写一个函数来检验它们是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

示例 1:
输入:       1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

输出: true

示例 2:
输入:      1          1
          /           \
         2             2

        [1,2],     [1,null,2]

输出: false


示例 3:
输入:       1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

输出: false
```

## <a name="chapter-three" id="chapter-three">三 解题 - 二叉树</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

```js
var isSameTree = function(p, q) {
  let serialize = function(root) {
    if (!root) {
      return '#!';
    }
    return `${root.val}!${serialize(root.left)}${serialize(root.right)}`;
  };
  return serialize(p) === serialize(q);
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



* 参数 `p`、`q`：

```js
var p = {
  val: 1,
  left: {
    val: 2,
    left: null,
    right: null,
  },
  right: {
    val: 1,
    left: null,
    right: null,
  },
}

var q = {
  val: 1,
  left: {
    val: 1,
    left: null,
    right: null,
  },
  right: {
    val: 2,
    left: null,
    right: null,
  },
}
```

* 返回值 `return`：

```js
false
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
√ Accepted
  √ 57/57 cases passed (76 ms)
  √ Your runtime beats 91.4 % of javascript submissions
  √ Your memory usage beats 23.48 % of javascript submissions (33.7 MB)
```

## <a name="chapter-six" id="chapter-six">六 解题思路</a>



**首先**，**jsliang** 和小伙伴们一样，都是首次接触二叉树，未免有点懵逼。

> 前端大佬除外，懂二叉树的除外~

**然后**，**jsliang** 进行了下打印，查看下为何如此解题：

```js
var isSameTree = function(p, q) {
  console.log('------\n原树：');
  console.log(p);
  console.log(q);
  let serialize = function(root) {
    if (!root) {
      return '#!';
    }
    return `${root.val}!${serialize(root.left)}${serialize(root.right)}`;
  };
  console.log('------\n现字符串：');
  console.log(serialize(p));
  console.log(serialize(q));
  return serialize(p) === serialize(q);
};
```

```
------
原树：
{ val: 1,
  left: { val: 2, left: null, right: null },
  right: { val: 1, left: null, right: null } }
{ val: 1,
  left: { val: 1, left: null, right: null },
  right: { val: 2, left: null, right: null } }
------
现字符串：
1!2!#!#!1!#!#!
1!1!#!#!2!#!#!
false
```

**最后**，看到这里，**jsliang** 感觉自己思路打开了大门，好像，二叉树的比较并不复杂嘛！（当然，仅限于比较，哈哈）

可以看到的是，我们通过递归，让树节点不断前行，就好比递归到 `p` 的最后一个节点 `right: { val: 1, left: null, right: null }`，这时候，我们通过 

```js
let serialize = function(root) {
  if (!root) {
    return '#!';
  }
  return `${root.val}!${serialize(root.left)}${serialize(root.right)}`;
};
```

来判断一个节点，是否还有子节点，到这最后一个节点的时候，因为 `root.left` 和 `root.right` 都是 `null`，所以触发 `if (!root) { ... }` 的条件，返回 `#!`（当然，这个不是固定的，你可以替换成其他字符串）。

那么，执行完这句，返回的就是 `1!#!#!`，再回看其他的节点，就一目明了了！

## <a name="chapter-seven" id="chapter-seven">七 进一步思考</a>



**不折腾的前端，和咸鱼有什么区别**

**jsliang** 每次解 LeetCode，都会先自己尝试破解，Submit 通过后，会查看下 LeetCode 社区其他小伙伴的破解思路，最后再看别人的代码，以此作为比较，吸取大神们的经验。

这次，由于第一次解树的题目，所以抱着虚心的心态，前往观摩，还真碰到了个不错的讲解：

* [写树算法的套路框架](https://leetcode-cn.com/problems/same-tree/solution/xie-shu-suan-fa-de-tao-lu-kuang-jia-by-wei-lai-bu-/)

> 由于原文采用 C++ 的编程风格，**jsliang** 引入的时候自动转换成 JavaScript。

以下是其内容：

---

二叉树算法的设计的总路线：明确一个节点要做的事情，然后剩下的事抛给框架。

```js
let traverse = function(root) {
  // root 需要做什么？在这做。
  // 其他的不用 root 操心，抛给框架
  traverse(root.left);
  traverse(root.right);
}
```

举两个简单的例子体会一下这个思路，热热身。

* 如何把二叉树所有的节点中的值加一？

```js
let plusOne = function(root) {
  if (!root) {
    return;
  }
  root.val += 1;

  plusOne(root.left);
  plusOne(root.right);
}
```

* 如何判断两棵二叉树是否完全相同？

```js
let isSameTree = function(root1, root2) {
  // 都为空的话，显然相同
  if (root1 == null && root2 == null) {
    return true;
  }
  // 一个为空，一个非空，显然不同
  if (root1 == null || root2 == null) {
    return false;
  }
  // 两个都非空，但 val 不一样也不行
  if (root1.val != root2.val) {
    return false;
  }
  
  // root1 和 root2 该比的都比完了，进行节点比较
  return isSameTree(root1.left, root2.left) && isSameTree(root1.right, root2.right);
}
```

---

大佬的解题套路如上，**jsliang** 觉得貌似有点道理，于是给记录下来，如果下次再碰到树，还能引用套路，无疑是件可喜的事！

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

