剑指 Offer 55 - I - 二叉树的深度
===

> Create by **jsliang** on **2020-08-21 16:17:25**  
> Recently revised in **2020-08-21 16:27:27**

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- |
| [一 目录](#chapter-one) |
| [二 题目](#chapter-two) |
| [三 解题思路](#chapter-three) |
| [四 解题套路](#chapter-four) |

## 二 题目



```
输入一棵二叉树的根节点，求该树的深度。

从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，
最长路径的长度为树的深度。

例如：

给定二叉树 [3,9,20,null,null,15,7]，

    3
   / \
  9  20
    /  \
   15   7

返回它的最大深度 3 。

提示：

* 节点总数 <= 10000

注意：本题与主站 104 题相同：https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

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
var maxDepth = function(root) {

};
```

根据上面的已知函数，小伙伴们可以先尝试破解本题，确定了自己的答案后再看下面代码。

## 三 解题思路



广度优先搜索：

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
const maxDepth = (root) => {
  // 狗不理
  if (!root) {
    return 0;
  }

  // 1. 设置深度为 0
  let depth = 0;

  // 2. 每层遍历
  let bfs = [root];

  // 3. 逐层访问树
  while (bfs.length) {
    // 3.1 每次遍历，深度 + 1
    depth++;

    // 3.2 设置下一次需要遍历的节点
    const tempBfs = [];
    
    // 3.3 遍历本次所有节点，将有内容的都添加进来
    for (let i = 0; i < bfs.length; i++) {
      if (bfs[i].left) {
        tempBfs.push(bfs[i].left);
      }
      if (bfs[i].right) {
        tempBfs.push(bfs[i].right);
      }
    }

    // 3.4 交接 tempBfs 到 bfs 上
    bfs = tempBfs;
  }

  // 4. 返回深度
  return depth;
};

const root = {
  val: 3,
  left: { val: 9 },
  right: {
    val: 20,
    left: { val: 15, left: null, right: null },
    right: { val: 7, left: null, right: null },
  },
};

console.log(maxDepth(root));
```

## 四 套路分析



本题暂未发现任何套路，如果有但是 **jsliang** 后面发现了的话，会在 GitHub 进行补充。

如果小伙伴有更好的思路想法，或者没看懂其中某种解法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](https://github.com/LiangJunrong/document-library/blob/master/public-repertory/img/z-index-small.png?raw=true)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

