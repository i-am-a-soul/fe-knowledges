剑指 Offer 32 - II - 从上到下打印二叉树 II
===

> Create by **jsliang** on **2020-09-04 10:48:51**  
> Recently revised in **2020-09-04 10:57:04**

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
从上到下按层打印二叉树，
同一层的节点按从左到右的顺序打印，
每一层打印到一行。

例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7

返回其层次遍历结果：
[
  [3],
  [9,20],
  [15,7]
]
 

提示：

节点总数 <= 1000
注意：本题与主站 102 题相同：https://leetcode-cn.com/problems/binary-tree-level-order-traversal/

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof
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
 * @return {number[][]}
 */
var levelOrder = function(root) {

};
```

根据上面的已知函数，小伙伴们可以先尝试破解本题，确定了自己的答案后再看下面代码。

## 三 解题思路



习惯成自然，广度优先搜索套个套路即可求解：

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
 * @return {number[][]}
 */
const levelOrder = (root) => {
  // 狗不理
  if (!root) {
    return [];
  }
  
  // 1. 设置结果集
  const result = [];

  // 2. 设置当前层
  let nowRoot = [root];

  // 3. 广度优先搜索（BFS）
  while (nowRoot.length) {
    // 3.1 设置下一层
    const nextRoot = [];

    // 3.2 设置当前层的值
    const nowResult = [];

    // 3.3 遍历当前层，取值以及添加下一层
    for (let i = 0; i < nowRoot.length; i++) {
      // 3.3.1 添加值
      nowResult.push(nowRoot[i].val);

      // 3.3.2 如果存在左子树
      if (nowRoot[i].left) {
        nextRoot.push(nowRoot[i].left);
      }

      // 3.3.3 如果存在右子树
      if (nowRoot[i].right) {
        nextRoot.push(nowRoot[i].right);
      }
    }

    // 3.4 收集完毕，开始交接
    nowRoot = nextRoot;
    result.push(nowResult);
  }

  // 4. 返回结果
  return result;
};

const root = {
  val: 3,
  left: { val: 9, left: null, right: null },
  right: {
    val: 20,
    left: { val: 15, left: null, right: null },
    right: { val: 7, left: null, right: null },
  },
};

console.log(levelOrder(root));
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

