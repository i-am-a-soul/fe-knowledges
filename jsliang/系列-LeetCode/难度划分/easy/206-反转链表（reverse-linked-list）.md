206 - 反转链表（reverse-linked-list）
===

> Create by **jsliang** on **2019-7-13 07:54:49**  
> Recently revised in **2019-7-13 08:42:07**

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
* **涉及知识**：链表
* **题目地址**：https://leetcode-cn.com/problems/reverse-linked-list/
* **题目内容**：

```
反转一个单链表。

示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL

进阶:
你可以迭代或递归地反转链表。你能否用两种方法解决这道题？
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var reverseList = (head, q = null) => {
  if (head) {
    return reverseList(head.next, {
      val: head.val,
      next: q,
    });
  }
  return q;
}
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



* `head`：

```js
let head = {
  val: 1, next: {
    val: 2, next: {
      val: 3, next: {
        val: 4, next: {
          val: 5, next: null,
        },
      },
    },
  },
};
```

* `return`：

```js
{
  val: 5, next: {
    val: 4, next: {
      val: 3, next: {
        val: 2, next: {
          val: 1, next: null,
        },
      },
    },
  },
}
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
√ Accepted
  √ 27/27 cases passed (80 ms)
  √ Your runtime beats 92.17 % of javascript submissions
  √ Your memory usage beats 6.29 % of javascript submissions (36.1 MB)
```

## <a name="chapter-six" id="chapter-six">六 解题思路</a>



**智商是硬伤，知识点也可能是**。

经过这次解题，**jsliang** 将链表给标记上了，等到系统学习算法与数据结构的时候，链表是必须搞懂的点之一。

**首先**，上面题解不是我写出来的，看的是评论区的题解，原代码是：

```js
const reverseList = (head, q = null) => head !== null ? reverseList(head.next, { val: head.val, next: q }) : q;
```

传说中的一行题解。

**然后**，怕小伙伴们跟我一样懵逼，**jsliang** 进行了改编：

```js
var reverseList = (head, q = null) => {
  console.log(q);
  if (head) {
    return reverseList(head.next, {
      val: head.val,
      next: q,
    });
  }
  return q;
}
```

**最后**，为了方便小伙伴们理解，**jsliang** 将 `q` 的过程打印了出来：

```js
null
{ val: 1, next: null }
{ val: 2, next: { val: 1, next: null } }
{ val: 3, next: { val: 2, next: { val: 1, next: null } } }
{ val: 4, next: { val: 3, next: { val: 2, next: [Object] } } }
{ val: 5, next: { val: 4, next: { val: 3, next: [Object] } } }
{ val: 5, next: { val: 4, next: { val: 3, next: [Object] } } }
```

嗯，对着 `console.log()` 来思考这次递归的用意，小伙伴们应该能清楚怎么反转链表了。（虽然下次还是可能写不出，但是没关系，后面大家一起系统学习~）

## <a name="chapter-seven" id="chapter-seven">七 进一步思考</a>



上面使用了递归，下面看看迭代解法：

```js
var reverseList = function(head) {
  if (head == null || head.next == null) {
    return head;
  }
  var current = head;
  var previous = null;
  while (current != null) {
    next = current.next;
    current.next = previous;
    previous = current;
    current = next;
  }
  return previous;
};
```

提交结果是：

```js
√ Accepted
  √ 27/27 cases passed (80 ms)
  √ Your runtime beats 92.17 % of javascript submissions
  √ Your memory usage beats 70.6 % of javascript submissions (34.8 MB)
```

感兴趣的小伙伴可以推演下迭代的思路，在此 **jsliang** 就不多滴滴啦~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

