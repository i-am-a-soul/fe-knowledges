933 - 最近的请求次数（number-of-recent-calls）
===

> Create by **jsliang** on **2020-01-27 10:52:42**  
> Recently revised in **2020-01-27 10:59:44**

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题及测试](#chapter-three) |
| [四 LeetCode Submit](#chapter-four) |
| [五 解题思路](#chapter-five) |

## 二 前言



* **难度**：简单
* **涉及知识**：队列
* **题目地址**：https://leetcode-cn.com/problems/number-of-recent-calls/
* **题目内容**：

```
写一个 RecentCounter 类来计算最近的请求。

它只有一个方法：ping(int t)，
其中 t 代表以毫秒为单位的某个时间。

返回从 3000 毫秒前到现在的 ping 数。

任何处于 [t - 3000, t] 时间范围之内的 ping 都将会被计算在内，
包括当前（指 t 时刻）的 ping。

保证每次对 ping 的调用都使用比之前更大的 t 值。

示例：

输入
inputs = ["RecentCounter","ping","ping","ping","ping"], 
inputs = [[],[1],[100],[3001],[3002]]
输出：[null,1,2,3,3]

提示：

每个测试用例最多调用 10000 次 ping。
每个测试用例会使用严格递增的 t 值来调用 ping。
每次调用 ping 都有 1 <= t <= 10^9。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/number-of-recent-calls
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
var RecentCounter = function() {
    
};

/** 
 * @param {number} t
 * @return {number}
 */
RecentCounter.prototype.ping = function(t) {
    
};

/** 
 * Your RecentCounter object will be instantiated and called as such:
 * var obj = new RecentCounter()
 * var param_1 = obj.ping(t)
 */
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
var RecentCounter = function() {
  this.val = [];
};

/** 
 * Your RecentCounter object will be instantiated and called as such:
 * var obj = new RecentCounter()
 * var param_1 = obj.ping(t)
 */
/** 
 * @param {number} t
 * @return {number}
 */
RecentCounter.prototype.ping = function(t) {
  this.val.push(t);
  while (this.val[0] < t - 3000){
    this.val.shift();
  }
  return this.val.length;
};
```

## 四 LeetCode Submit



```js
Accepted
* 68/68 cases passed (408 ms)
* Your runtime beats 35.29 % of javascript submissions
* Your memory usage beats 95.96 % of javascript submissions (56.1 MB)
```

## 五 解题思路



设计模式 0 分渣渣路过：

> 不知名求解

```js
var RecentCounter = function() {
  this.val = [];
};

/** 
 * Your RecentCounter object will be instantiated and called as such:
 * var obj = new RecentCounter()
 * var param_1 = obj.ping(t)
 */
/** 
 * @param {number} t
 * @return {number}
 */
RecentCounter.prototype.ping = function(t) {
  this.val.push(t);
  while (this.val[0] < t - 3000){
    this.val.shift();
  }
  return this.val.length;
};
```

Submit 提交如下：

```js
Accepted
* 68/68 cases passed (408 ms)
* Your runtime beats 35.29 % of javascript submissions
* Your memory usage beats 95.96 % of javascript submissions (56.1 MB)
```

1. 我没看懂题意
2. 感觉对设计模式不是很熟
3. 科比去世了（2020-01-27）

乱糟糟的，原谅我这一次水了~

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

