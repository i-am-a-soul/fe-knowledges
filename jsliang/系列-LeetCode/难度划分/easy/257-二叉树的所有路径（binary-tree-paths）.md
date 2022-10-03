257 - 二叉树的所有路径（binary-tree-paths）
===

> Create by **jsliang** on **2019-07-18 10:15:11**  
> Recently revised in **2019-09-18 13:47:43**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| [四 执行测试](#chapter-four) |
| [五 LeetCode Submit](#chapter-five) |
| [六 知识点](#chapter-six) |
| [七 解题思路](#chapter-seven) |
| [八 进一步思考](#chapter-eight) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：树、深度优先搜索
* **题目地址**：https://leetcode-cn.com/problems/binary-tree-paths/
* **题目内容**：

```
给定一个二叉树，返回所有从根节点到叶子节点的路径。

说明: 叶子节点是指没有子节点的节点。

示例:

输入:
   1
 /   \
2     3
 \
  5
输出: ["1->2->5", "1->3"]

解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var binaryTreePaths = function(root) {
  let result = [];
  const ergodic = function(root, path) {
    if (!root) {
      return;
    }
    path = path + root.val + (root.left || root.right ? '->' : '');
    if (!root.left && !root.right) {
      result.push(path);
      return;
    }
    ergodic(root.left, path);
    ergodic(root.right, path);
  };
  ergodic(root, '');
  return result;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



* `root`：

```js
const root = {
  val: 1,
  left: {
    val: 2,
    left: null,
    right: { val: 5, left: null, right: null },
  },
  right: { val: 3, left: null, right: null },
};
```

* `return`：

```js
[ '1->2->5', '1->3' ]
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
✔ Accepted
  ✔ 209/209 cases passed (84 ms)
  ✔ Your runtime beats 82.32 % of javascript submissions
  ✔ Your memory usage beats 66 % of javascript submissions (34.3 MB)
```

## <a name="chapter-six" id="chapter-six">六 知识点</a>



1. `push()`：`push()` 方法将一个或多个元素添加到数组的末尾，并返回该数组的新长度。[`push()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Array/push.md)

## <a name="chapter-seven" id="chapter-seven">七 解题思路</a>



**首先**，还是提下我们的万能公式：

```js
const ergodic = function(root) {
  if (!root) {
    return;
  }
  ergodic(root.left);
  ergodic(root.right);
}
```

将一棵树丢进去，它会遍历这棵树中的所有节点。

**然后**，我们解析下代码：

```js
var binaryTreePaths = function(root) {
  let result = [];
  const ergodic = function(root, path) {
    if (!root) {
      return;
    }
    path = path + root.val + (root.left || root.right ? '->' : '');
    if (!root.left && !root.right) {
      result.push(path);
      return;
    }
    ergodic(root.left, path);
    ergodic(root.right, path);
  };
  ergodic(root, '');
  return result;
};
```

1. 定义 `result` 来接收最终结果。
2. 定义 `path` 来接收每次到叶子节点（叶子节点是指这个节点的左节点和右节点都为空的最终节点）时，这条路径的长度。
3. 将 `root` 丢进万能公式中遍历，不同的是，添加多一个 `path` 节点。
4. 最终，我们的 `result` 会获取到所有的内容。

**最后**，我们将 `result` 给返回出去即可。

## <a name="chapter-eight" id="chapter-eight">八 进一步思考</a>



当然，我们可以吸取下其他小伙伴/大佬的解法，毕竟集思广益，说不定对你下次解题有帮助：

> 参考 1：递归

```js
var binaryTreePaths = function (root) {
  if (!root) return [];
  if (!root.left && !root.right) {
    return [root.val + ''];
  }
  let left = binaryTreePaths(root.left).map(key => root.val + '->' + key);
  let right = binaryTreePaths(root.right).map(key => root.val + '->' + key);
  return left.concat(right);
};
```

> 参考 2：递归

```js
var binaryTreePaths = function (root) {
  var res = [];

  function dfs(root, str) {
    if (!root) return;
    str += root.val;
    if (!root.left && !root.right) {
      res.push(str);
      return;
    }
    str += '->';
    dfs(root.left, str);
    dfs(root.right, str);
  }
  dfs(root, '');
  return res;
};
```

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

