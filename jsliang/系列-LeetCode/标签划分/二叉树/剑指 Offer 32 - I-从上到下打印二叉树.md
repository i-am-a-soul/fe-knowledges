剑指 Offer 32 - I - 从上到下打印二叉树
===

> Create by **jsliang** on **2020-09-04 10:33:04**  
> Recently revised in **2020-09-04 10:43:22**

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
从上到下打印出二叉树的每个节点，
同一层的节点按照从左到右的顺序打印。

例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7

返回：
[3,9,20,15,7]
 

提示：

节点总数 <= 1000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof
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
 * @return {number[]}
 */
var levelOrder = function(root) {

};
```

根据上面的已知函数，小伙伴们可以先尝试破解本题，确定了自己的答案后再看下面代码。

## 三 解题思路



* 广度优先搜索（BFS）

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
 * @return {number[]}
 */
const levelOrder = (root) => {
  // 狗不理
  if (!root) {
    return [];
  }
  
  // 1. 设置结果集
  const result = [];

  // 2. 设置当前层（要遍历的位置）
  let nowRoot = [root];

  // 3. 如果当前层还需要遍历
  while (nowRoot.length) {
    // 3.1 设置下一层
    const nextRoot = [];

    // 3.2 遍历当前层，提取当前层的值以及获取下一层的值
    for (let i = 0; i < nowRoot.length; i++) {
      // 3.2.1 添加值到 result 中
      result.push(nowRoot[i].val);

      // 3.2.2 如果有左子树
      if (nowRoot[i].left) {
        nextRoot.push(nowRoot[i].left);
      }

      // 3.2.3 如果有右子树
      if (nowRoot[i].right) {
        nextRoot.push(nowRoot[i].right);
      }
    }

    // 3.3 交接下一层到当前层
    nowRoot = nextRoot;
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

console.log(levelOrder(root)); // [ 3, 9, 20, 15, 7 ]
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

