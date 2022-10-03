234 - 回文链表（palindrome-linked-list）
===

> Create by **jsliang** on **2019-07-16 19:21:54**  
> Recently revised in **2019-09-18 13:46:06**

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
* **涉及知识**：链表、双指针
* **题目地址**：https://leetcode-cn.com/problems/palindrome-linked-list/
* **题目内容**：

```
请判断一个链表是否为回文链表。

示例 1:
输入: 1->2
输出: false

示例 2:
输入: 1->2->2->1
输出: true

进阶：
你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var isPalindrome = function(head) {
  let result = [];
  while (head) {
    result.push(head.val);
    head = head.next;
  }
  for (let i = 0; i < result.length / 2; i++) {
    if (result[i] !== result[result.length - 1 - i]) {
      return false;
    }
  }
  return true;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



* `head`：

```js
const head = {
  val: 1, next: {
    val: 2, next: {
      val: 2, next: {
        val: 1,
      },
    },
  },
};
```

* `return`：

```js
true
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
✔ Accepted
  ✔ 26/26 cases passed (84 ms)
  ✔ Your runtime beats 94.25 % of javascript submissions
  ✔ Your memory usage beats 50 % of javascript submissions (39.7 MB)
```

## <a name="chapter-six" id="chapter-six">六 知识点</a>



1. `push()`：`push()` 方法将一个或多个元素添加到数组的末尾，并返回该数组的新长度。[`push()` 详细介绍](https://github.com/LiangJunrong/document-library/blob/master/JavaScript-library/JavaScript/%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1/Array/push.md)

## <a name="chapter-seven" id="chapter-seven">七 解题思路</a>



**要相信你的直觉**。

**首先**，拿到题目的第一时间，我想到的就是：**将链表抽取成数组，然后判断数组是否为回文**。

```js
while (head) {
  result.push(head.val);
  head = head.next;
}
```

**然后**，我们只需要遍历一半的数组（因为回文意味着左右相等），坐标 `0` 对应 `length - 1 - 0`，坐标 `1` 对应 `length - 1 - 1`，坐标 `i` 对应 `length - 1 - i`：

```js
for (let i = 0; i < result.length / 2; i++) {
  if (result[i] !== result[result.length - 1 - i]) {
    return false;
  }
}
```

**最后**，我们如果遍历了还是 OK，则返回 `true`。

OK，直接很准确~

## <a name="chapter-eight" id="chapter-eight">八 进一步思考</a>



那么，除了双指针形式，还有其他的吗？

有的！

> 递归：

```js
var isPalindrome = function(head, queue = []) {
  if (!head) {
    return true;
  }
  queue.push(head.val);
  let flag = isPalindrome(head.next, queue);
  return queue.shift() === head.val && flag;
}
```

当然，方法不止一种，**jsliang** 这里就不做过多讲解和展示啦~

有思路的小伙伴可以留言或者评论哈~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

