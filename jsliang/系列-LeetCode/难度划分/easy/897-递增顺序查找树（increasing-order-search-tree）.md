897 - 递增顺序查找树（increasing-order-search-tree）
===

> Create by **jsliang** on **2020-01-19 09:04:26**  
> Recently revised in **2020-01-19 09:33:11**

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
* **涉及知识**：树、深度优先搜索
* **题目地址**：
* **题目内容**：

```
给定一个树，
按中序遍历重新排列树，
使树中最左边的结点现在是树的根，
并且每个结点没有左子结点，
只有一个右子结点。

 

示例 ：

输入：[5,3,6,2,4,null,8,1,null,null,null,7,9]

       5
      / \
    3    6
   / \    \
  2   4    8
 /        / \ 
1        7   9

输出：[1,null,2,null,3,null,4,null,5,null,6,null,7,null,8,null,9]

 1
  \
   2
    \
     3
      \
       4
        \
         5
          \
           6
            \
             7
              \
               8
                \
                 9  
 

提示：

给定树中的结点数介于 1 和 100 之间。
每个结点都有一个从 0 到 1000 范围内的唯一整数值。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var islandPerimeter = function(grid) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
function TreeNode(val) {
  this.val = val;
  this.left = this.right = null;
}
/**
 * @name 递增顺序查找树
 * @param {TreeNode} root
 * @return {TreeNode}
 */
const increasingBST = (root) => {
  const result = new TreeNode();
  let current = result;
  const ergodic = (root) => {
    if (!root) {
      return;
    }
    ergodic(root.left);
    root.left = null;
    current.right = root;
    current = root;
    ergodic(root.right);
  };
  ergodic(root);

  return result.right;
};

const root = {
  val: 3,
  left: {
    val: 2,
    left: { val: 1, left: null, right: null },
    right: null,
  },
  right: { val: 4, left: null, right: null },
};

console.log(increasingBST(root));
// { val: 1,
//   left: null,
//   right:
//    { val: 2,
//      left: null,
//      right: { val: 3, left: null, right: [Object] } } }
```

`node index.js` 返回：

```js
{
  val: 1,
  left: null,
  right:
   { val: 2,
     left: null,
     right: {
       val: 3,
       left: null,
       right: {
         val: 4,
         left: null,
         right: {
           val: 5,
           left: null,
           right: null,
         }
       },
    },
  },
}
```

## 四 LeetCode Submit



```js
Accepted
* 2156/2156 cases passed (152 ms)
* Your runtime beats 88.71 % of javascript submissions
* Your memory usage beats 10 % of javascript submissions (43.9 MB)
```

## 五 解题思路



**首先**，拿下题目关键字：

* 按中序遍历
* 只有一个右子结点

那么，开干：

```js
/**
 * @name 构造一颗简单树
 * @param {*} val 传入的值
 */
function TreeNode(val) {
  this.val = val;
  this.left = this.right = null;
}

/**
 * @name 递增顺序查找树
 * @param {TreeNode} root
 * @return {TreeNode}
 */
const increasingBST = (root) => {
  const result = new TreeNode();
  let current = result;
  const ergodic = (root) => {
    if (!root) {
      return;
    }
    ergodic(root.left);
    root.left = null;
    current.right = root;
    current = root;
    ergodic(root.right);
  };
  ergodic(root);

  return result.right;
};
```

思路如下：

1. 通过 `result` 生成一颗新树；
2. 通过 `current` 控制树的走向；
3. 通过 `ergodic` 递归遍历树；
4. 遍历到 `!root` 的时候终止；
5. 先遍历所有的左节点，将其取出来，设置当前节点左节点为 `null`，然后设置 `current` 的右节点为该节点 `root`。
6. 遍历这棵树右节点。

我们通过 `console` 查看：

> 打 console

```js
const increasingBST = (root) => {
  const result = new TreeNode();
  let current = result;
  const ergodic = (root) => {
    if (!root) {
      return;
    }
    console.log('------');
    console.log(root);
    console.log(current);
    ergodic(root.left);
    root.left = null;
    current.right = root;
    current = root;
    ergodic(root.right);
  };
  ergodic(root);

  return result.right;
};
```

> console 打印结果

```
------
{ val: 3,
  left:
   { val: 2,
     left: { val: 1, left: null, right: null },
     right: null },
  right: { val: 4, left: null, right: null } }
TreeNode { val: undefined, right: null, left: null }

------
{ val: 2,
  left: { val: 1, left: null, right: null },
  right: null }
TreeNode { val: undefined, right: null, left: null }

------
{ val: 1, left: null, right: null }
TreeNode { val: undefined, right: null, left: null }

------
{ val: 4, left: null, right: null }
{ val: 3,
  left: null,
  right: { val: 4, left: null, right: null } }
```

很好，这样我们就了解了这个走向~

Submit 提交：

```js
Accepted
* 2156/2156 cases passed (152 ms)
* Your runtime beats 88.71 % of javascript submissions
* Your memory usage beats 10 % of javascript submissions (43.9 MB)
```

## 六 进一步思考



更多的比较好的方法，我看这个大佬写得非常好：

* 三种与中序遍历相关的方法：https://leetcode-cn.com/problems/increasing-order-search-tree/solution/san-chong-yu-zhong-xu-bian-li-xiang-guan-de-fang-f/

如果小伙伴有更多的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

