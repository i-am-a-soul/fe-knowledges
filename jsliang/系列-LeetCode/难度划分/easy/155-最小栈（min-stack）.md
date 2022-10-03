155 - 最小栈（min-stack）
===

> Create by **jsliang** on **2019-07-03 16:40:04**  
> Recently revised in **2019-07-03 19:29:55**

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

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：栈、设计
* **题目地址**：https://leetcode-cn.com/problems/min-stack/
* **题目内容**：

```
设计一个支持 push，pop，top 操作，并能在常数时间内检索到最小元素的栈。

push(x) -- 将元素 x 推入栈中。
pop() -- 删除栈顶的元素。
top() -- 获取栈顶元素。
getMin() -- 检索栈中的最小元素。

示例:
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码**：

```js
var MinStack = function () {
  this.stack = [];
  this.min = null;
};

MinStack.prototype.push = function (x) {
  this.stack.push(x);
  if (this.min === null) {
    this.min = x;
  } else {
    this.min = Math.min(this.min, x);
  }
};

MinStack.prototype.pop = function () {
  this.stack.pop();
  this.min = this.stack.length ? this.stack.reduce((min, num) => Math.min(min, num), Infinity) : null;
};

MinStack.prototype.top = function () {
  if (!this.stack.length) {
    return null;
  }
  return this.stack[this.stack.length - 1];
};

MinStack.prototype.getMin = function () {
  return this.min;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



```js
let minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
let nowMin = minStack.getMin();
console.log('现在最小：' + nowMin);
minStack.pop();
let nowTop = minStack.top();
console.log('现在顶部：' + nowTop);
let newMin = minStack.getMin();
console.log(minStack);
console.log('现在最小：' + newMin);
```

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
✔ Accepted
  ✔ 18/18 cases passed (148 ms)
  ✔ Your runtime beats 97.72 % of javascript submissions
  ✔ Your memory usage beats 48.3 % of javascript submissions (44.2 MB)
```

## <a name="chapter-six" id="chapter-six">六 解题思路</a>



**首先**，上手直接开撸：

```js
var MinStack = function() {
  this.stack = [];
};

MinStack.prototype.push = function(x) {
  this.stack.push(x);
};

MinStack.prototype.pop = function() {
  this.stack.pop();
};

MinStack.prototype.top = function() {
  if (!this.stack.length) {
    return null;
  }
  return this.stack[this.stack.length - 1];
};

MinStack.prototype.getMin = function() {
  return this.stack.slice().sort((a, b) => a - b)[0];
};
```

一开始我的思路是这样的，然后 LeetCode 提交返回：

```js
✘ Time Limit Exceeded
  ✘ 17/18 cases passed (N/A)
  ✘ testcase: '["MinStack","push","push",……]'
  ✘ answer: 
  ✘ expected_answer: 
  ✘ stdout:
```

好家伙，超时限制！！！

**接着**，发现它还会提出 JS 最大值超范围的数字，范围限制！！！

**最后**，感觉不太耐烦了，直接找大佬的代码了。

> 有的小伙伴说我没有讲解每句话的意思，其实这道题总体来说没有任何难点

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

