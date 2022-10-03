994 - 腐烂的橘子（rotting-oranges）
===

> Create by **jsliang** on **2020-01-28 19:43:29**  
> Recently revised in **2020-01-28 22:50:53**

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
* **涉及知识**：广度优先搜索
* **题目地址**：https://leetcode-cn.com/problems/rotting-oranges/
* **题目内容**：

在给定的网格中，每个单元格可以有以下三个值之一：

* 值 0 代表空单元格；
* 值 1 代表新鲜橘子；
* 值 2 代表腐烂的橘子。

每分钟，任何与腐烂的橘子（在 4 个正方向上）相邻的新鲜橘子都会腐烂。

返回直到单元格中没有新鲜橘子为止所必须经过的最小分钟数。

如果不可能，返回 -1。

---

示例 1：

![图](../../../public-repertory/img/other-algorithm-994-1.png)

输入：

```
[
  [2,1,1],
  [1,1,0],
  [0,1,1]
]
```

输出：4

---

示例 2：

输入：

```
[
  [2,1,1],
  [0,1,1],
  [1,0,1]
]
```

输出：-1

解释：左下角的橘子（第 2 行， 第 0 列）永远不会腐烂，因为腐烂只会发生在 4 个正向上。

---

示例 3：

输入：[[0,2]]

输出：0

解释：因为 0 分钟时已经没有新鲜橘子了，所以答案就是 0 。

---

提示：

1 <= grid.length <= 10
1 <= grid[0].length <= 10
grid[i][j] 仅为 0、1 或 2

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/rotting-oranges

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var orangesRotting = function(grid) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 腐烂的橘子
 * @param {number[][]} grid
 * @return {number}
 */
const orangesRotting = (grid) => {
  // 1. 获取可以感染的清单
  let canInfectionList = [];
  for (let i = 0; i < grid.length; i++) {
    for (let j = 0; j < grid[i].length; j++) {
      if (grid[i][j] === 1) {
        canInfectionList.push(`${i}${j}`);
      }
    }
  }
  // 2. 开始感染
  let time = 0;
  let flag = false;
  while (canInfectionList.length && !flag) {
    const infectionList = []; // 2.1 即将感染清单
    for (let i = 0; i < grid.length; i++) {
      for (let j = 0; j < grid[i].length; j++) {
        if (grid[i][j] === 2) {
          if (grid[i - 1] && grid[i - 1][j] === 1) {
            infectionList.push([i - 1, j]);
          }
          if (grid[i + 1] && grid[i + 1][j] === 1) {
            infectionList.push([i + 1, j]);
          }
          if (grid[i][j - 1] === 1) {
            infectionList.push([i, j - 1]);
          }
          if (grid[i][j + 1] === 1) {
            infectionList.push([i, j + 1]);
          }
        }
      }
    }
    // 2.2 如果存在即将感染的清单，感染次数 + 1
    if (infectionList.length) {
      time ++;
    }
    // 2.3 将即将感染清单上的项进行感染，同时过滤 canInfectionList 这个可以感染的清单
    for (let i = 0; i < infectionList.length; i++) {
      grid[infectionList[i][0]][infectionList[i][1]] = 2;
      canInfectionList = canInfectionList.filter(item => item !== `${infectionList[i][0]}${infectionList[i][1]}`);
    }
    // 2.4 如果没有即将感染的清单，同时还剩下可以感染的情况，需要特殊处理，返回 -1
    if (!infectionList.length && canInfectionList.length) {
      flag = true;
    }
  }
  // 3. 返回不能完全感染或者感染全部需要的次数
  return flag ? -1 : time;
};

console.log(orangesRotting(
  [
    [2, 1, 1],
    [1, 1, 0],
    [0, 1, 1],
  ],
)); // 4
console.log(orangesRotting(
  [[0], [2]],
)); // 0
console.log(orangesRotting(
  [[2], [0], [2]],
)); // 0
console.log(orangesRotting(
  [[1, 2, 1, 1, 2, 1, 1]],
)); // 2
console.log(orangesRotting(
  [[2], [2], [1], [0], [1], [1]],
)); // -1
console.log(orangesRotting(
  [[0]],
)); // 0
console.log(orangesRotting(
  [
    [1,0,2,1,2,1,2],
    [1,0,0,2,1,0,1]
  ],
)); // -1
```

`node index.js` 返回：

```js
4
0
0
2
-1
0
-1
```

## 四 LeetCode Submit



```js
Accepted
* 303/303 cases passed (108 ms)
* Your runtime beats 27.4 % of javascript submissions
* Your memory usage beats 14 % of javascript submissions (38 MB)
```

## 五 解题思路



头皮发麻，看了下题目，尝试破解了下，表明这道题应该属于中等难度了！！！

这道题有点玩《瘟疫公司》的感觉，需要不停去感染。

> 暴力破解

```js
const orangesRotting = (grid) => {
  // 1. 获取可以感染的清单
  let canInfectionList = [];
  for (let i = 0; i < grid.length; i++) {
    for (let j = 0; j < grid[i].length; j++) {
      if (grid[i][j] === 1) {
        canInfectionList.push(`${i}${j}`);
      }
    }
  }
  // 2. 开始感染
  let time = 0;
  let flag = false;
  while (canInfectionList.length && !flag) {
    const infectionList = []; // 2.1 即将感染清单
    for (let i = 0; i < grid.length; i++) {
      for (let j = 0; j < grid[i].length; j++) {
        if (grid[i][j] === 2) {
          if (grid[i - 1] && grid[i - 1][j] === 1) {
            infectionList.push([i - 1, j]);
          }
          if (grid[i + 1] && grid[i + 1][j] === 1) {
            infectionList.push([i + 1, j]);
          }
          if (grid[i][j - 1] === 1) {
            infectionList.push([i, j - 1]);
          }
          if (grid[i][j + 1] === 1) {
            infectionList.push([i, j + 1]);
          }
        }
      }
    }
    // 2.2 如果存在即将感染的清单，感染次数 + 1
    if (infectionList.length) {
      time ++;
    }
    // 2.3 将即将感染清单上的项进行感染，同时过滤 canInfectionList 这个可以感染的清单
    for (let i = 0; i < infectionList.length; i++) {
      grid[infectionList[i][0]][infectionList[i][1]] = 2;
      canInfectionList = canInfectionList.filter(item => item !== `${infectionList[i][0]}${infectionList[i][1]}`);
    }
    // 2.4 如果没有即将感染的清单，同时还剩下可以感染的情况，需要特殊处理，返回 -1
    if (!infectionList.length && canInfectionList.length) {
      flag = true;
    }
  }
  // 3. 返回不能完全感染或者感染全部需要的次数
  return flag ? -1 : time;
};
```

解题思路如下：

1. 首先，假设我们是都可以感染的，所以应该存在 `canInfectionList`，里面是所有的可以感染的目标（1）。
2. 然后，我们 `while (canInfectionList.length && !flag) {}`，这里的 `canInfectionList` 表明剩下可被感染的清单；`flag` 表明是否还能继续感染下去。
3. 接着，我们设置 `infectionList` 表示本次即将感染的清单，用来统计感染源上下左右为 1 的地址。
4. 再来，判断 `infectionList` 本次即将感染的清单是否存在，如果存在，说明本次可以感染，`time++`，同时，将即将感染清单的目标进行感染，将剩下可被感染的清单进行过滤。
5. 同时，判断如果 `infectionList` 本次即将感染的清单不存在，但是 `canInfectionList` 还存在，那么说明感染不下去了，需要返回 `-1`。
6. 其他情况返回 `time` 即可。

Submit 提交如下：

```js
Accepted
* 303/303 cases passed (108 ms)
* Your runtime beats 27.4 % of javascript submissions
* Your memory usage beats 14 % of javascript submissions (38 MB)
```

写完大脑宕机，就不评论【题解区】和【评论区】了~

## 六 进一步思考



留下悔恨的泪水，历史记录下自己失败的一幕。

这份题解，花了我 2 个半钟。

在第 2 个钟的时候，我以为我写不下去了，最接近的答案是下面的代码。

我内心感到无奈和苦恼，为什么这道题这么复杂~

然后，稍微瞄了一眼【题解区】的答案，就一眼，没详看，我发现它也差不多那么长，于是我就想自己到底能不能独立破解，于是回头继续搞，换个思路重新出发。

终于，我在 2 个半钟的时候，凭借自己的垃圾思路成功破解~

下面是那份代码，记录我失败的一面。

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

> 失败有许许多多的次数，但是这次我印象特深

```js
/**
 * @name 腐烂的橘子
 * @param {number[][]} grid
 * @return {number}
 */
const orangesRotting = (grid) => {
  // 1. 排除不能全部感染的状态
  let map = [];
  let twoFlag = '没有感染源'; // 假设存在感染源，而不是 [[1], [1], [1], [1]]
  let oneRow = '', oneVertical = '';
  // [[2, 0, 1, 2, 0, 1]]
  if (grid.length === 1) {
    grid[0].forEach(item => oneRow += item);
  }
  for (let i = 0; i < grid.length; i++) {
    // [[2], [0], [1], [2], [0], [1]]
    if (grid[i].length === 1) {
      oneVertical += grid[i][0];
    }
    for (let j = 0; j < grid[i].length; j++) {
      if (
        grid[i][j] === 1
        && !(grid[i - 1] && grid[i - 1][j])
        && !(grid[i + 1] && grid[i + 1][j])
        && !grid[i][j - 1]
        && !grid[i][j + 1]
      ) {
        return -1;
      }
      if (grid[i][j] === 1) {
        map.push(`${i}${j}`);
      }
      if (grid[i][j] === 2) {
        twoFlag = '有感染源';
      }
    }
  }
  const oneRowList = oneRow.split('0');
  if (oneRowList.length >= 2) {
    for (let i = 0; i < oneRowList.length; i++) {
      if (!oneRowList[i].includes('2') && oneRowList[i].includes('1')) {
        return -1;
      }
    }
  }
  const oneVerticalList = oneVertical.split('0');
  if (oneVerticalList.length >= 2) {
    for (let i = 0; i < oneVerticalList.length; i++) {
      if (!oneVerticalList[i].includes('2') && oneVerticalList[i].includes('1')) {
        return -1;
      }
    }
  }
  if (grid.length === 1 && grid[0].length === 1 && grid[0][0] === 0) {
    return 0;
  }
  if (twoFlag === '没有感染源') {
    return -1;
  }
  // 2. 正常全部能感染的状态
  let time = 0;
  while (map.length) {
    console.log('------');
    console.log(map);
    console.log(grid);
    const infectionList = []; // 即将感染清单
    for (let i = 0; i < grid.length; i++) {
      for (let j = 0; j < grid[i].length; j++) {
        if (grid[i][j] === 2) {
          if (grid[i - 1] && grid[i - 1][j] === 1) {
            infectionList.push([i - 1, j]);
          }
          if (grid[i + 1] && grid[i + 1][j] === 1) {
            infectionList.push([i + 1, j]);
          }
          if (grid[i][j - 1] === 1) {
            infectionList.push([i, j - 1]);
          }
          if (grid[i][j + 1] === 1) {
            infectionList.push([i, j + 1]);
          }
        }
      }
    }
    if (infectionList.length) {
      time ++;
    }
    for (let i = 0; i < infectionList.length; i++) {
      grid[infectionList[i][0]][infectionList[i][1]] = 2;
      map = map.filter(item => item !== `${infectionList[i][0]}${infectionList[i][1]}`);
    }
  }
  return time;
};

// console.log(orangesRotting(
//   [
//     [2, 1, 1],
//     [1, 1, 0],
//     [0, 1, 1],
//   ],
// )); // 4
// console.log(orangesRotting(
//   [[0], [2]],
// )); // 0
// console.log(orangesRotting(
//   [[2], [0], [2]],
// )); // 0
// console.log(orangesRotting(
//   [[1, 2, 1, 1, 2, 1, 1]],
// )); // 2
// console.log(orangesRotting(
//   [[2], [2], [1], [0], [1], [1]],
// )); // -1
// console.log(orangesRotting(
//   [[0]],
// )); // 0
console.log(orangesRotting(
  [
    [1,0,2,1,2,1,2],
    [1,0,0,2,1,0,1]
  ],
)); // 0
```

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

