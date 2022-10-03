141 - 环形链表（linked-list-cycle）
===

> Create by **jsliang** on **2019-7-3 08:10:25**  
> Recently revised in **2019-7-3 08:52:02**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：链表、双指针
* **题目地址**：https://leetcode-cn.com/problems/linked-list-cycle/
* **题目内容**：

```
给定一个链表，判断链表中是否有环。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

示例 1：
输入：head = [3,2,0,-4], pos = 1
输出：true
解释：链表中有一个环，其尾部连接到第二个节点。

示例 2：
输入：head = [1,2], pos = 0
输出：true
解释：链表中有一个环，其尾部连接到第一个节点。

示例 3：
输入：head = [1], pos = -1
输出：false
解释：链表中没有环。 

进阶：

你能用 O(1)（即，常量）内存解决此问题吗？
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



第一眼看题，**没懂**

不对，再瞅瞅，**还是没懂**

难道，我想错了？看下题解，**还还是没懂**

这我就震惊了，我不会是遇到假题目了吧~

看下代码：

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *   this.val = val;
 *   this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {boolean}
 */
var hasCycle = function(head) {
    
};
```

enm...怎么只有 `head`，那个 `pos` 呢？

回头看了下题解：

* 官方题解：https://leetcode-cn.com/problems/linked-list-cycle/solution/huan-xing-lian-biao-by-leetcode/
* 个人题解：https://leetcode-cn.com/problems/linked-list-cycle/solution/8mskuai-man-zhi-zhen-hashsi-lu-de-go-shi-xian-by-e/

> 比较有意思的题解：

```js
var hasCycle = function(head) {
  while (head) {
    if (head.val === 'jsliang') {
      return true;
    } else {
      head.val = 'jsliang';
    }
    head = head.next;
  }
  return false;
};
```

```js
√ Accepted
  √ 17/17 cases passed (84 ms)
  √ Your runtime beats 98.59 % of javascript submissions
  √ Your memory usage beats 75.67 % of javascript submissions (36.4 MB)
```

凉了凉了，怎么它们讲得头头是道，我却连题目都不懂~

无解，放着，等回头系统学下算法与数据结构的书，再看看是不是我哪里出问题了。

小伙伴们如果对这道题有个人见解，可以提出来，感谢分享~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

