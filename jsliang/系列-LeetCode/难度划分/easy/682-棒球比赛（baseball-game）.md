682 - 棒球比赛（baseball-game）
===

> Create by **jsliang** on **2019-12-13 07:59:55**  
> Recently revised in **2019-12-13 08:55:37**

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
* **涉及知识**：栈
* **题目地址**：https://leetcode-cn.com/problems/baseball-game/
* **题目内容**：

```
你现在是棒球比赛记录员。
给定一个字符串列表，每个字符串可以是以下四种类型之一：
1.整数（一轮的得分）：直接表示您在本轮中获得的积分数。
2. "+"（一轮的得分）：表示本轮获得的得分是前两轮有效 回合得分的总和。
3. "D"（一轮的得分）：表示本轮获得的得分是前一轮有效 回合得分的两倍。
4. "C"（一个操作，这不是一个回合的分数）：
表示您获得的最后一个有效 回合的分数是无效的，应该被移除。

每一轮的操作都是永久性的，可能会对前一轮和后一轮产生影响。
你需要返回你在所有回合中得分的总和。

示例 1:

输入: ["5","2","C","D","+"]
输出: 30
解释: 
第 1 轮：你可以得到 5 分。总和是：5。
第 2 轮：你可以得到 2 分。总和是：7。
操作 1：第 2 轮的数据无效。总和是：5。
第 3 轮：你可以得到 10 分（第2轮的数据已被删除）。总数是：15。
第 4 轮：你可以得到 5 + 10 = 15分。总数是：30。

示例 2:

输入: ["5","-2","4","C","D","9","+","+"]
输出: 27
解释: 
第 1 轮：你可以得到 5 分。总和是：5。
第 2 轮：你可以得到 -2 分。总数是：3。
第 3 轮：你可以得到 4 分。总和是：7。
操作 1：第3轮的数据无效。总数是：3。
第 4 轮：你可以得到 -4 分（第三轮的数据已被删除）。总和是：-1。
第 5 轮：你可以得到 9 分。总数是：8。
第 6 轮：你可以得到 -4 + 9 = 5分。总数是 13。
第 7 轮：你可以得到 9 + 5 = 14分。总数是 27。
注意：

输入列表的大小将介于 1 和 1000 之间。
列表中的每个整数都将介于 -30000 和 30000 之间。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string[]} ops
 * @return {number}
 */
var calPoints = function(ops) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 棒球比赛
 * @param {string[]} ops
 * @return {number}
 */
const calPoints = (ops) => {
  let result = 0;
  for (let i = 0; i < ops.length; i++) {
    // 正常得分
    if (Number.isInteger(Number(ops[i])) && ops[i + 1] !== 'C') {
      result += Number(ops[i]);
      ops[i] = Number(ops[i]);
    } else if (ops[i] === 'C') { // 'C' - 删除得分
      result -= Number(ops[i - 1]);
      ops.splice(i - 1, 2);
      i -= 2;
    } else if (ops[i + 1] === 'C') { // 'C' - 删除得分
      ops.splice(i, 2);
      i--;
    } else if (ops[i] === 'D' && ops[i - 1]) { // 'D' - 前一轮有效得分的两倍
      result += Number(ops[i - 1] * 2);
      ops[i] = Number(ops[i - 1] * 2);
    } else if (ops[i] === '+') { // '+' - 前两轮有效得分的和
      result += Number(ops[i - 2] + ops[i - 1]);
      ops[i] = Number(ops[i - 2] + ops[i - 1]);
    }
  }
  return result;
};

console.log(calPoints(['5', '2', 'C', 'D', '+'])); // 30
console.log(calPoints(['5', '-2', '4', 'C', 'D', '9', '+', '+'])); // 27
console.log(calPoints(['4', 'D', 'D', 'C', 'D'])); // 28
console.log(calPoints(['-60','D','-36','30','13','C','C','-33','53','79'])); // -117
console.log(calPoints(['10','20','30','40','C','C','C'])); // -117
```

`node index.js` 返回：

```js
30
27
28
-117
10
```

## 四 LeetCode Submit



```js
Accepted
* 39/39 cases passed (84 ms)
* Your runtime beats 25.94 % of javascript submissions
* Your memory usage beats 39.24 % of javascript submissions (35.2 MB)
```

## 五 解题思路



**鬼知道我经历了什么，就是 if...if...if 跑完了题目。**

> 暴力破解

```js
const calPoints = (ops) => {
  let result = 0;
  for (let i = 0; i < ops.length; i++) {
    // 正常得分
    if (Number.isInteger(Number(ops[i])) && ops[i + 1] !== 'C') {
      result += Number(ops[i]);
      ops[i] = Number(ops[i]);
    } else if (ops[i] === 'C') { // 'C' - 删除得分
      result -= Number(ops[i - 1]);
      ops.splice(i - 1, 2);
      i -= 2;
    } else if (ops[i + 1] === 'C') { // 'C' - 删除得分
      ops.splice(i, 2);
      i--;
    } else if (ops[i] === 'D' && ops[i - 1]) { // 'D' - 前一轮有效得分的两倍
      result += Number(ops[i - 1] * 2);
      ops[i] = Number(ops[i - 1] * 2);
    } else if (ops[i] === '+') { // '+' - 前两轮有效得分的和
      result += Number(ops[i - 2] + ops[i - 1]);
      ops[i] = Number(ops[i - 2] + ops[i - 1]);
    }
  }
  return result;
};
```

是的，你没看错，就是一对的 `if...else if...` 判断，其他正常得分啊、'D'、'+' 啊还好，有一种情况：

* `['10', '10', '10', 'C', 'C']`

这种，会让你猝不及防，因为删除后面的一个 `'C'` 后，下一轮到的还是 `'C'`，于是不得不加上判断：

```js
else if (ops[i] === 'C') { // 'C' - 删除得分
  result -= Number(ops[i - 1]);
  ops.splice(i - 1, 2);
  i -= 2;
} 
```

就是防止删除 `'C'` 后，本轮还是 `'C'`。

详细的我就不说了，按照正常的题目规则走即可。

## 六 进一步思考



这道题肯定还有更有意思的解法。

但是我被恶心到了，然后今天有两道题解，所以如果你对这道题有想法，欢迎评论留言或者私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

