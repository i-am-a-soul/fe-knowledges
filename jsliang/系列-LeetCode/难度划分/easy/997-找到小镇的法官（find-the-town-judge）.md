997 - 找到小镇的法官（find-the-town-judge）
===

> Create by **jsliang** on **2020-01-29 10:43:10**  
> Recently revised in **2020-01-29 11:18:00**

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
* **涉及知识**：图
* **题目地址**：https://leetcode-cn.com/problems/find-the-town-judge/
* **题目内容**：

```
在一个小镇里，按从 1 到 N 标记了 N 个人。

传言称，这些人中有一个是小镇上的秘密法官。

如果小镇的法官真的存在，那么：

小镇的法官不相信任何人。
每个人（除了小镇法官外）都信任小镇的法官。
只有一个人同时满足属性 1 和属性 2 。
给定数组 trust，
该数组由信任对 trust[i] = [a, b] 组成，
表示标记为 a 的人信任标记为 b 的人。

如果小镇存在秘密法官并且可以确定他的身份，
请返回该法官的标记。

否则，返回 -1。 

示例 1：

输入：N = 2, trust = [[1,2]]
输出：2

示例 2：

输入：N = 3, trust = [[1,3],[2,3]]
输出：3

示例 3：

输入：N = 3, trust = [[1,3],[2,3],[3,1]]
输出：-1

示例 4：

输入：N = 3, trust = [[1,2],[2,3]]
输出：-1

示例 5：

输入：N = 4, trust = [[1,3],[1,4],[2,3],[2,4],[4,3]]
输出：3

提示：

1 <= N <= 1000
trust.length <= 10000
trust[i] 是完全不同的
trust[i][0] != trust[i][1]
1 <= trust[i][0], trust[i][1] <= N

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-the-town-judge
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} N
 * @param {number[][]} trust
 * @return {number}
 */
var findJudge = function(N, trust) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 找到小镇的法官
 * @param {number} N
 * @param {number[][]} trust
 * @return {number}
 */
const findJudge = (N, trust) => {
  // 1. 哈希表：记录村民（信任别人的人）
  const villagerMap = new Set();
  // 2. 哈希表：记录法官（被信任的人）
  const judgeMap = new Map();
  // 3. 遍历信任清单，进行哈希记忆
  for (let i = 0; i < trust.length; i++) {
    const trusted = trust[i][1];
    const time = judgeMap.get(trusted);
    villagerMap.add(trust[i][0]);
    if (time) {
      judgeMap.set(trusted, time + 1);
    } else {
      judgeMap.set(trusted, 1);
    }
  }
  // 4. 开始汇报结果
  for (let [key, value] of judgeMap) {
    if (value === N - 1 && !villagerMap.has(key)) {
      return key;
    }
  }

  return !trust.length ? N : -1;
};

console.log(findJudge(4, [[1, 3], [1, 4], [2, 3], [2, 4], [4, 3]])); // 3
```

`node index.js` 返回：

```js
3
```

## 四 LeetCode Submit



```js
Accepted
* 89/89 cases passed (120 ms)
* Your runtime beats 62 % of javascript submissions
* Your memory usage beats 39.13 % of javascript submissions (43.8 MB)
```

## 五 解题思路



这道题还是挺新奇的：

1. 有数组 `[[1, 2], [1, 3], [2, 3]]`。
2. 数组每个元素中，例如 `[1, 2]`，1 表示村民，2 表示它信任的人。
3. 如果被信任的人共同是一个人，那么这个人是法官：`[[1, 2], [1, 3], [2, 3]]`，法官是 3。
4. 如果被信任的人还信任另一个人，那么这个人不是法官：`[[1, 2], [1, 3], [2, 3], [3, 1]]`。

这样，我们就窃取了本题机密，开始暴力破解：

> 暴力破解

```js
const findJudge = (N, trust) => {
  // 1. 哈希表：记录村民（信任别人的人）
  const villagerMap = new Set();
  // 2. 哈希表：记录法官（被信任的人）
  const judgeMap = new Map();
  // 3. 遍历信任清单，进行哈希记忆
  for (let i = 0; i < trust.length; i++) {
    // 3.1 当前被信任的人
    const trusted = trust[i][1];
    // 3.2 当前被信任的次数
    const time = judgeMap.get(trusted);
    // 3.3 哈希表：记录每个村民
    villagerMap.add(trust[i][0]);
    // 3.4 哈希表：统计法官次数
    if (time) {
      judgeMap.set(trusted, time + 1);
    } else {
      judgeMap.set(trusted, 1);
    }
  }
  // 4. 开始汇报结果
  for (let [key, value] of judgeMap) {
    // 4.1 如果被信任次数为 N - 1
    // 4.2 如果它不在村民清单中
    if (value === N - 1 && !villagerMap.has(key)) {
      return key;
    }
  }
  // 5. 如果找不到，返回 -1
  // 6. 如果存在 findJudge(1, []) 情况
  return !trust.length ? N : -1;
};
```

如上，**jsliang** 给你安排地清清楚楚了~

Submit 提交如下：

```js
Accepted
* 89/89 cases passed (120 ms)
* Your runtime beats 62 % of javascript submissions
* Your memory usage beats 39.13 % of javascript submissions (43.8 MB)
```

如果小伙伴觉得自己思路更清晰，亦或者提交的结果更完美，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

