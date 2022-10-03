083 - 删除排序链表中的重复元素（remove-duplicates-from-sorted-list）
===

> Create by **jsliang** on **2019-6-12 08:50:11**  
> Recently revised in **2019-6-12 09:26:06**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题代码](#chapter-three) |
| [四 执行测试](#chapter-four) |
| [五 LeetCode Submit](#chapter-five) |
| [六 解题思路](#chapter-six) |
| [七 总结](#chapter-seven) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：链表
* **题目地址**：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/
* **题目内容**：

```
给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

示例 1:

输入: 1->1->2
输出: 1->2
示例 2:

输入: 1->1->2->3->3
输出: 1->2->3
```

## <a name="chapter-three" id="chapter-three">三 解题代码</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

```js
var deleteDuplicates = function(head) {
  if (!head) { // 预防 [] 情况
    return head;
  }
  let removal = {
    val: -99, // 预防 [-1, 1, 1, 1, 3] 情况 
    next: null,
  };
  let follower = removal;
  while (head) {
    if (head.val != follower.val) {
      follower.next = head;
      head = head.next;
      follower = follower.next;
    } else {
      if (head.next === null) { // 预防 [1, 1, 2, 3, 3] 情况
        follower.next = null;
      }
      head = head.next;
    }
  }
  return removal.next;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



* 参数：`head`：

```js
let head = {
  val: 1,
  next: {
    val: 1,
    next: {
      val: 2,
      next: {
        val: 3,
        next: {
          val: 3,
          next: null
        }
      },
    }
  }
}
```

* 返回值： `return`：

```js
{ val: 1, next: { val: 2, next: { val: 3, next: null } } }
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
√ Accepted
  √ 165/165 cases passed (100 ms)
  √ Your runtime beats 90.76 % of javascript submissions
  √ Your memory usage beats 13.09 % of javascript submissions (36.3 MB)
```

## <a name="chapter-six" id="chapter-six">六 解题思路</a>



**首先**，这道题不是第一次碰到链表，小伙伴可以查看 [021-合并两个有序链表（merge-two-sorted-lists）](https://github.com/LiangJunrong/document-library/blob/master/other-library/LeetCode/easy/021-%E5%90%88%E5%B9%B6%E4%B8%A4%E4%B8%AA%E6%9C%89%E5%BA%8F%E9%93%BE%E8%A1%A8%EF%BC%88merge-two-sorted-lists%EF%BC%89.md)，先了解一波链表的有关知识。

**然后**，在这道题中，我们的解题思路就可以迎刃而解了：

* **步骤 1**：在代码中添加 `console.log()`，查看代码执行机制。

```js
var deleteDuplicates = function(head) {
  if (!head) { // 预防 [] 情况
    return head;
  }
  let removal = {
    val: -99, // 预防 [-1, 1, 1, 1, 3] 情况 
    next: null,
  };
  let follower = removal;
  while (head) {
    console.log('------');
    console.log(head);
    console.log(removal);
    console.log(follower);
    if (head.val != follower.val) {
      follower.next = head;
      head = head.next;
      follower = follower.next;
    } else {
      if (head.next === null) { // 预防 [1, 1, 2, 3, 3] 情况
        follower.next = null;
      }
      head = head.next;
    }
  }
  return removal.next;
};

let head = { // 即 [1, 1, 2, 3, 3]
  val: 1,
  next: {
    val: 1,
    next: {
      val: 2,
      next: {
        val: 3,
        next: {
          val: 3,
          next: null
        }
      },
    }
  }
}

deleteDuplicates(head);
```

* **步骤 2**：执行代码，得到打印信息，顺序 `head` -> `removal` -> `follower`。

```js
jsliang 注释：
  第一次遍历，
  我们的 head、removal、follower 都处于初始状态
------
{ val: 1, next: { val: 1, next: { val: 2, next: { val: 3, next: { val: 3, next: null } } } } }
{ val: -99, next: null }
{ val: -99, next: null }

jsliang 注释：
  第二次遍历，
  我们的 head = head.next，follower = head.next，
  这样 removal 就获得了 1，以及之后的整个 next。
------
{ val: 1, next: { val: 2, next: { val: 3, next: { val: 3, next: null } } } }
{ val: -99, next: { val: 1, next: { val: 1, next: { val: 2, next: { val: 3, next: { val: 3, next: null } } } } } }
{ val: 1, next: { val: 1, next: { val: 2, next: { val: 3, next: { val: 3, next: null } } } } }

jsliang 注释：
  第三次遍历，
  我们的 head 继续前进一步：head = head.next，
  但是因为 head.val == follower.val，
  所以我们这次不修改 follower，从而做到去重的作用。
  （follower 的变动影响 removal 的变动）
------
{ val: 2, next: { val: 3, next: { val: 3, next: null } } }
{ val: -99, next: { val: 1, next: { val: 1, next: { val: 2, next: { val: 3, next: { val: 3, next: null } } } } } }
{ val: 1, next: { val: 1, next: { val: 2, next: { val: 3, next: { val: 3, next: null } } } } }

jsliang 注释：
  第四次遍历，
  我们的 head 继续前进一步：head = head.next，
  然后 follower 和 removal 获得了 head.next。
------
{ val: 3, next: { val: 3, next: null } }
{ val: -99, next: { val: 1, next: { val: 2, next: { val: 3, next: { val: 3, next: null } } } } }
{ val: 2, next: { val: 3, next: { val: 3, next: null } } }

jsliang 注释：
  第五次遍历，
  我们的 head 继续前进一步：head = head.next，
  此时 head.val == follower.val，
  并且 head.next == null，
  所以我们直接将 follower.next 设置为 null，
  从而获得最终结果
------
{ val: 3, next: null }
{ val: -99, next: { val: 1, next: { val: 2, next: { val: 3, next: { val: 3, next: null } } } } }
{ val: 3, next: { val: 3, next: null } }

jsliang 注释：
  最终 return 的值如下所示：
------
{ val: 1, next: { val: 2, next: { val: 3, next: null } } }
```

**最后**，小伙伴们如果还不理解，可以自行拷贝代码到本地，或者看多两遍代码，如有不懂，记得留言。

## <a name="chapter-seven" id="chapter-seven">七 总结</a>



这样，我们就搞定了 LeetCode 简单难度的第二个链表题目，想来也就那么回事，小伙伴们学会了吗~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

