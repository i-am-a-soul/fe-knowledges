面试题 30 - 包含 min 函数的栈
===

> Create by **jsliang** on **2020-07-19 21:01:39**  
> Recently revised in **2020-7-19 21:23:02**  

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- |
| [一 目录](#chapter-one) |
| [二 题目](#chapter-two) |
| [三 解题思路](#chapter-three) |
| [四 统计分析](#chapter-four) |
| [五 解题套路](#chapter-five) |

## 二 题目



```
定义栈的数据结构，
请在该类型中实现一个
能够得到栈的最小元素的 min 函数在该栈中，
调用 min、push 及 pop 的时间复杂度都是 O(1)。

示例:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.

提示：

各函数的调用总次数不超过 20000 次

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```js
/**
 * initialize your data structure here.
 */
var MinStack = function() {
  
};

/** 
 * @param {number} x
 * @return {void}
 */
MinStack.prototype.push = function(x) {

};

/**
 * @return {void}
 */
MinStack.prototype.pop = function() {

};

/**
 * @return {number}
 */
MinStack.prototype.top = function() {

};

/**
 * @return {number}
 */
MinStack.prototype.min = function() {

};

/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(x)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.min()
 */
```

根据上面的已知函数，小伙伴们可以先尝试破解本题，确定了自己的答案后再看下面代码。

## 三 解题思路



```js
const MinStack = function() {
  this.items = [];
  this.length = 0;
  this.minStack = [];
  this.push = (x) => {
    this.items.push(x);
    this.length++;
    const minLength = this.minStack.length;
    if (!minLength || x <= this.minStack[minLength - 1]) {
      this.minStack.push(x);
    } else if (x > this.minStack[minLength - 1]) {
      this.minStack.push(this.minStack[minLength - 1]);
    }
  };
  this.pop = () => {
    this.items.pop();
    this.length--;
    this.minStack.pop();
  };
  this.top = () => {
    return this.items[this.length - 1];
  };
  this.min = (x) => {
    return this.minStack[this.minStack.length - 1];
  };
};

/*
const minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
console.log(minStack.min()); // 返回 -3.
minStack.pop();
console.log(minStack.top()); // 返回 0.
console.log(minStack.min()); // 返回 -2.
*/
```

## 四 统计分析



本题不需要统计分析。

## 五 套路分析



本题暂未发现任何套路，如果有但是 **jsliang** 后面发现了的话，会在 GitHub 进行补充。

如果小伙伴有更好的思路想法，或者没看懂其中某种解法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](https://github.com/LiangJunrong/document-library/blob/master/public-repertory/img/z-index-small.png?raw=true)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

