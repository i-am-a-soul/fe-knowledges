657 - 机器人能否返回原点（robot-return-to-origin）
===

> Create by **jsliang** on **2019-12-06 08:39:44**  
> Recently revised in **2019-12-06 09:07:41**

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题及测试](#chapter-three) |
| [四 LeetCode Submit](#chapter-four) |
| [五 解题思路](#chapter-five) |
| [六 进一步思考](#chapter-six) |

## 二 前言



* **难度**：简单
* **涉及知识**：字符串
* **题目地址**：https://leetcode-cn.com/problems/robot-return-to-origin/
* **题目内容**：

```
在二维平面上，有一个机器人从原点 (0, 0) 开始。

给出它的移动顺序，判断这个机器人在完成移动后是否在 (0, 0) 处结束。

移动顺序由字符串表示。

字符 move[i] 表示其第 i 次移动。

机器人的有效动作有 R（右），L（左），U（上）和 D（下）。

如果机器人在完成所有动作后返回原点，则返回 true。

否则，返回 false。

注意：机器人“面朝”的方向无关紧要。

“R” 将始终使机器人向右移动一次，“L” 将始终向左移动等。
 
此外，假设每次移动机器人的移动幅度相同。

示例 1:

输入: "UD"
输出: true
解释：
机器人向上移动一次，然后向下移动一次。
所有动作都具有相同的幅度，因此它最终回到它开始的原点。
因此，我们返回 true。

示例 2:

输入: "LL"
输出: false
解释：
机器人向左移动两次。
它最终位于原点的左侧，距原点有两次 “移动” 的距离。
我们返回 false，因为它在移动结束时没有返回原点。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} moves
 * @return {boolean}
 */
var judgeCircle = function(moves) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 机器人能否返回圆点
 * @param {string} moves
 * @return {boolean}
 */
const judgeCircle = (moves) => {
  const position = [0, 0];
  for (let i = 0; i < moves.length; i++) {
    switch (moves[i]) {
      case 'U':
        position[1] += 1;
        break;
      case 'R':
        position[0] += 1;
        break;
      case 'D':
        position[1] -= 1;
        break;
      case 'L':
        position[0] -= 1;
        break;
    }
  }
  return position[0] === 0 && position[1] === 0;
};

console.log(judgeCircle('UD')); // true
console.log(judgeCircle('LL')); // false
```

`node index.js` 返回：

```js
true
false
```

## 四 LeetCode Submit



```js
Accepted
* 63/63 cases passed (68 ms)
* Your runtime beats 94.94 % of javascript submissions
* Your memory usage beats 64.91 % of javascript submissions (36.5 MB)
```

## 五 解题思路



**送分题！**

建立坐标 `[0, 0]`：

```
      |
      |
----[0, 0]---
      |
      |
```

剩下的就简单了，就是走过 `moves` 步后，回到 `[0, 0`]。

> 第一次提交

```js
const judgeCircle = (moves) => {
  const position = [0, 0];
  for (let i = 0; i < moves.length; i++) {
    switch (moves[i]) {
      case 'U':
        position[1] += 1;
        break;
      case 'R':
        position[0] += 1;
        break;
      case 'D':
        position[1] -= 1;
        break;
      case 'L':
        position[0] -= 1;
        break;
    }
  }
  return position[0] === 0 && position[1] === 0;
};
```

分析一下：

1. 原点为 `[0, 0]`。
2. 向上移动为 `[0, 1]`，即 `position[1] += 1`；
3. 向右移动为 `[1, 0]`，即 `position[0] += 1`；
4. 向下移动为 `[0, -1]`，即 `position[1] -= 1`；
5. 向左移动为 `[-1, 0]`，即 `position[0] -= 1`；
6. 遍历步骤，产生上面代码，最后判断两个坐标点是否都为 0 即可。

Submit 提交：

```js
Accepted
* 63/63 cases passed (68 ms)
* Your runtime beats 94.94 % of javascript submissions
* Your memory usage beats 64.91 % of javascript submissions (36.5 MB)
```

搞定，收工~

## 六 进一步思考



顺带看看【题解区】和【评论区】的奇技淫巧：

> 【题解区】1

```js
const judgeCircle = (moves) => {
  // 判断左右移动的次数和上下移动的次数是否相等（即 L.count === R.count && U.count === D.count）
  return moves.split('L').length === moves.split('R').length && moves.split('U').length === moves.split('D').length
};
```

Submit 提交：

```js
Accepted
* 63/63 cases passed (84 ms)
* Your runtime beats 45.89 % of javascript submissions
* Your memory usage beats 21.93 % of javascript submissions (39.7 MB)
```

* 优点：一行代码
* 缺点：进行了 4 次分割，即上面我写的代码的 4 倍工作。

> 【题解区】2

```js
const judgeCircle = (moves) => {
  var o = 0;
  var v = 0;
  for (var i = 0; i < moves.length; i++) {
    switch (moves[i]) {
      case 'L':
        o--;
        break;
      case 'R':
        o++;
        break;
      case 'U':
        v++;
        break;
      case 'D':
        v--;
        break;
    }
  }
  return !o && !v;
};
```

Submit 提交：

```js
Accepted
* 63/63 cases passed (76 ms)
* Your runtime beats 74.37 % of javascript submissions
* Your memory usage beats 93.86 % of javascript submissions (35.5 MB)
```

跟 **jsliang** 代码差不多，区别在于使用 数组 还是 数字 来存储数据。

以上，就是本题的所有内容啦~

如果小伙伴有更好的思路或者想法，欢迎留言评论或者私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

