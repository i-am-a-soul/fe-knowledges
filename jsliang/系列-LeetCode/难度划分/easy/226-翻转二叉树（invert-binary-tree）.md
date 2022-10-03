226 - 翻转二叉树（invert-binary-tree）
===

> Create by **jsliang** on **2019-07-15 10:49:55**  
> Recently revised in **2019-07-15 11:43:24**

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
* **题目地址**：https://leetcode-cn.com/problems/invert-binary-tree/
* **题目内容**：

```
翻转一棵二叉树。

示例：

输入：
     4
   /   \
  2     7
 / \   / \
1   3 6   9

输出：
     4
   /   \
  7     2
 / \   / \
9   6 3   1

备注:

这个问题是受到 Max Howell 的 原问题 启发的 ：

谷歌：我们 90％ 的工程师使用您编写的软件(Homebrew)，
但是您却无法在面试时在白板上写出翻转二叉树这道题，这太糟糕了。
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var invertTree = function(root) {
  if (!root) {
    return null;
  }
  return {
    val: root.val,
    left: invertTree(root.right) || null,
    right: invertTree(root.left) || null,
  }
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



* `root`：

```js
const root = {
  val: 4,
  left: 
  { val: 2,
    left: { val: 1, left: null, right: null },
    right: { val: 3, left: null, right: null },
  },
  right: 
  { val: 7,
    left: { val: 6, left: null, right: null },
    right: { val: 9, left: null, right: null },
  },
};
```

* `return`：

```js
{ val: 4,
  left:
   { val: 7,
     left: { val: 9, left: null, right: null },
     right: { val: 6, left: null, right: null } },
  right:
   { val: 2,
     left: { val: 3, left: null, right: null },
     right: { val: 1, left: null, right: null } } }
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
✔ Accepted
  ✔ 68/68 cases passed (72 ms)
  ✔ Your runtime beats 93.87 % of javascript submissions
  ✔ Your memory usage beats 39.65 % of javascript submissions (33.7 MB)
```

## <a name="chapter-six" id="chapter-six">六 解题思路</a>



**首先**，很久没破解树的题了，那么咱从远古时代开始说起吧：

* **树的万能公式**：

```js
let ergodic = function(root) {
  // root 需要做什么？在这做。
  // 其他的不用 root 操心，抛给框架
  ergodic(root.left);
  ergodic(root.right);
}
```

OK，什么意思呢？

我们编写一个方法，将树丢进去，然后不断递归，遍历这棵树，得到最终结果。

话再多比不上代码，那么根据本题上代码带大家过过：

```js
const root = {
  val: 4,
  left: {
    val: 2,
    left: { val: 1, left: null, right: null },
    right: { val: 3, left: null, right: null },
  },
  right: {
    val: 7,
    left: { val: 6, left: null, right: null },
    right: { val: 9, left: null, right: null },
  },
};

var invertTree = function(root) {
  let ergodic = function(root) {
    if (!root) {
      return '!#';
    }
    return '!' + root.val + ergodic(root.left) + ergodic(root.right);
  };
  return ergodic(root);
};

console.log(invertTree(root));
```

小伙伴们可以先想想它会返回什么：

```js
!4!2!1!#!#!3!#!#!7!6!#!#!9!#!#
```

很好，大家学到了个 **前序遍历**（先根节点，再左子树，最后右子树）。

那么，本题需要翻转二叉树，我们调整下顺序即可：

```js
return '!' + root.val + ergodic(root.right) + ergodic(root.left);
```

它就返回：

```js
!4!7!9!#!#!6!#!#!2!3!#!#!1!#!#
```

OK，我们成功翻转遍历了，那么我们是否可以尝试下，修改它返回的结果：

```js
var invertTree = function(root) {
  let ergodic = function(root) {
    if (!root) {
      return null;
    }
    return {
      val: root.val,
      left: ergodic(root.right) || null,
      right: ergodic(root.left) || null,
    }
  };
  return ergodic(root);
};
```

现在查看下结果是否是我们需要的：

```js
{ val: 4,
  left:
   { val: 7,
     left: { val: 9, left: null, right: null },
     right: { val: 6, left: null, right: null } },
  right:
   { val: 2,
     left: { val: 3, left: null, right: null },
     right: { val: 1, left: null, right: null } } }
```

perfect！我们成功完成了树的翻转，但是我们还有个问题：**如何将内部遍历修改为原地遍历，干掉一切能产生的变量，提高运行速度和减低内存占用率**。

```js
var invertTree = function(root) {
  if (!root) {
    return null;
  }
  return {
    val: root.val,
    left: invertTree(root.right) || null,
    right: invertTree(root.left) || null,
  }
};
```

是的，经过多次的思考变动，我们得出最后的结果。

## <a name="chapter-seven" id="chapter-seven">七 进一步思考</a>



在上面题解中，我们通过递归的形式，一步一步破解了本题。

那么，除此之外，我们还有其他方法吗？

有的，迭代！

但是由于迭代方面，**jsliang** 使用的不多，不够熟练，这里就不献丑了，如果小伙伴们写了出来，可以提交到留言或者评论~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

