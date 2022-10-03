237 - 删除链表中的节点（delete-node-in-a-linked-list）
===

> Create by **jsliang** on **2019-07-17 16:54:11**  
> Recently revised in **2019-07-17 17:30:39**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| [四 LeetCode Submit](#chapter-four) |
| [五 解题思路](#chapter-five) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：链表
* **题目地址**：https://leetcode-cn.com/problems/delete-node-in-a-linked-list/
* **题目内容**：

```
请编写一个函数，使其可以删除某个链表中给定的（非末尾）节点，你将只被给定要求被删除的节点。

现有一个链表 -- head = [4,5,1,9]，它可以表示为:

4 --> 5 --> 1 --> 9 

示例 1:
输入: head = [4,5,1,9], node = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.

示例 2:
输入: head = [4,5,1,9], node = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.

说明:
链表至少包含两个节点。
链表中所有节点的值都是唯一的。
给定的节点为非末尾节点并且一定是链表中的一个有效节点。
不要从你的函数中返回任何结果。
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var deleteNode = function(node) {
  node.val = node.next.val;
  node.next = node.next.next;
};
```

## <a name="chapter-four" id="chapter-four">四 LeetCode Submit</a>



```js
✔ Accepted
  ✔ 41/41 cases passed (144 ms)
  ✔ Your runtime beats 10.41 % of javascript submissions
  ✔ Your memory usage beats 98.49 % of javascript submissions (35.2 MB)
```

## <a name="chapter-five" id="chapter-five">五 解题思路</a>



**这道题的解题思路，就是没有思路**！

**首先**，这道题就是脑经急转弯：

```js
var deleteNode = function(node) {
  // ...
};
```

它给的代码上，标明传的参是 `node`，所以 **jsliang** 就懵圈了，这是想干啥。

**然后**，我开始逛论坛，骂的老惨了：

https://leetcode-cn.com/problems/delete-node-in-a-linked-list/comments/

官方题解的意思就是：**与下一个节点交换**。

所以，答案就是：

```js
var deleteNode = function(node) {
  node.val = node.next.val;
  node.next = node.next.next;
};
```

**最后**，怎么想都想不透，这智商锅我背不背~

> 真心不是 **jsliang** 想水题解，而是……真的题目很水。

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

