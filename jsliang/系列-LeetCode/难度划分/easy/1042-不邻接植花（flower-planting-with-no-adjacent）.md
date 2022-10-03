1042 - 不邻接植花（flower-planting-with-no-adjacent）
===

> Create by **jsliang** on **2020-01-30 16:59:45**  
> Recently revised in **2020-01-30 20:52:47**

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
* **题目地址**：https://leetcode-cn.com/problems/flower-planting-with-no-adjacent/
* **题目内容**：

```
有 N 个花园，按从 1 到 N 标记。

在每个花园中，你打算种下四种花之一。

paths[i] = [x, y] 描述了花园 x 到花园 y 的双向路径。

另外，没有花园有 3 条以上的路径可以进入或者离开。

你需要为每个花园选择一种花，
使得通过路径相连的任何两个花园中的花的种类互不相同。

以数组形式返回选择的方案作为答案 answer，
其中 answer[i] 为在第 (i+1) 个花园中种植的花的种类。
花的种类用  1, 2, 3, 4 表示。

保证存在答案。

示例 1：

输入：N = 3, paths = [[1,2],[2,3],[3,1]]
输出：[1,2,3]

示例 2：

输入：N = 4, paths = [[1,2],[3,4]]
输出：[1,2,1,2]

示例 3：

输入：N = 4, paths = [[1,2],[2,3],[3,4],[4,1],[1,3],[2,4]]
输出：[1,2,3,4]

提示：

1 <= N <= 10000
0 <= paths.size <= 20000
不存在花园有 4 条或者更多路径可以进入或离开。
保证存在答案。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/flower-planting-with-no-adjacent
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} N
 * @param {number[][]} paths
 * @return {number[]}
 */
var gardenNoAdj = function(N, paths) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 不邻接植花
 * @param {number} N
 * @param {number[][]} paths
 * @return {number[]}
 */
const gardenNoAdj = (N, paths) => {
  // 1. 构造通道，索引 0 对应花园 1
  const gardenPath = Array.from(Array(N), () => []);
  
  // 2. 填充数据
  for (let i = 0; i < paths.length; i++) {
    gardenPath[paths[i][0] - 1].push(paths[i][1]);
    gardenPath[paths[i][1] - 1].push(paths[i][0]);
  }
  
  // 3. 开始挖坑，拿好花种
  const result = Array.from(Array(N), () => '');
  const flowers = [1, 2, 3, 4];

  // 4. 开始填坑
  for (let i = 0; i < gardenPath.length; i++) {
    const path = gardenPath[i].map(item => result[item - 1]);
    const canUse = Array.from(new Set([...flowers].filter(item => !path.includes(item))));
    result[i] = canUse[0];
  }

  // 5. 去掉没用的坑
  return result;
};

console.log(gardenNoAdj(3, [[1, 2], [2, 3], [3, 1]])); // [1, 2, 3]
console.log(gardenNoAdj(3, [[2, 3], [1, 3], [2, 1]])); // [1, 2, 3]

console.log(gardenNoAdj(4, [[1, 2], [2, 3], [3, 4], [4, 1], [1, 3], [2, 4]])); // [1, 2, 3, 4]
console.log(gardenNoAdj(4, [[1, 2], [3, 4]])); // [1, 2, 1, 2]
console.log(gardenNoAdj(4, [[1, 2], [3, 4], [3, 2], [4, 2], [1, 4]])); // [1, 2, 1, 3]

console.log(gardenNoAdj(5, [[4, 1], [4, 2], [4, 3], [2, 5], [1, 2], [1, 5]])); // [1, 2, 1, 3, 3]

console.log(gardenNoAdj(6, [[1, 2], [1, 4], [2, 4], [3, 4], [2, 6], [6, 1]])); // [1, 2, 1, 3, 1, 3]
```

`node index.js` 返回：

```js
[ 1, 2, 3 ]
[ 1, 2, 3 ]
[ 1, 2, 3, 4 ]
[ 1, 2, 1, 2 ]
[ 1, 2, 1, 3 ]
[ 1, 2, 1, 3, 3 ]
[ 1, 2, 1, 3, 1, 3 ]
```

## 四 LeetCode Submit



```js
Accepted
* 51/51 cases passed (240 ms)
* Your runtime beats 16.67 % of javascript submissions
* Your memory usage beats 16.67 % of javascript submissions (73.5 MB)
```

## 五 解题思路



有时候 LeetCode 题目的描述令人诟病，你是知道的：

* 没有花园有 3 条以上的路径可以进入或者离开。
* 不存在花园有 4 条或者更多路径可以进入或离开。

那就是不存在 [4, n) 路径了。

……

> FBI warning：这道题是中等难度，LeetCode 放到简单难度就是想折腾你

……

经过近 3 小时的折腾，终于搞出套路：

> 暴力破解【未简化】

```js
const gardenNoAdj = (N, paths) => {
  // 1. 构造通道
  const gardenMap = Array.from(Array(N), (value, index) => {
    return {
      garden: index + 1,
      path: [],
    };
  });
  
  // 2. 填充数据
  for (let i = 0; i < paths.length; i++) {
    gardenMap[paths[i][0] - 1].path.push(paths[i][1]);
    gardenMap[paths[i][1] - 1].path.push(paths[i][0]);
  }
  
  // 3. 开始挖坑，拿好花种
  const result = Array.from(Array(N + 1), () => '');
  const flowers = [1, 2, 3, 4];

  // 4. 开始填坑
  for (let i = 0; i < gardenMap.length; i++) {
    const values = [];
    for (let j = 0; j < gardenMap[i].path.length; j++) {
      const k = gardenMap[i].path[j];
      values.push(result[k]);
    }
    const canUse = Array.from(new Set([...flowers].filter(x => !values.includes(x))));
    result[i + 1] = canUse[0];
  }

  // 5. 去掉没用的坑
  result.shift();
  return result;
};
```

拿 `[[1, 2], [1, 4], [2, 4], [3, 4], [2, 6], [6, 1]]` 分析：

**首先**，步骤 1 + 步骤 2，生成数据：

```js
[
  { garden: 1, path: [ 2, 4, 6 ] },
  { garden: 2, path: [ 1, 4, 6 ] },
  { garden: 3, path: [ 4 ] },
  { garden: 4, path: [ 1, 2, 3 ] },
  { garden: 5, path: [] },
  { garden: 6, path: [ 2, 1 ] },
]
```

这时候我们知道，哪个花园可以通向哪个花园。

**然后**，我们开始挖坑和设置花种：

```js
['', '', '', '', '', '', '']
[1, 2, 3, 4]
```

需要注意的是，为了保持索引的一致性，这里我们加了个表示 0 的坑，最后会通过 `result.shift()` 清空掉。

**接着**，开始填坑：

```
1 => ['', 1, '', '', '', '', '']
2 => ['', 1,  2, '', '', '', '']
3 => ['', 1,  2,  1, '', '', '']
4 => ['', 1,  2,  1,  3, '', '']
5 => ['', 1,  2,  1,  3,  1, '']
6 => ['', 1,  2,  1,  3,  1,  1]
```

可以看到，我们通过 `values` 获取了当前花园通向其他花园的值，然后我们通过 `canUse` 取 `values` 和 `flowers` 的差集，表明我们剩余可用的花种有多少。

这时候，知道剩余可用花种，我们用第一种就行了。

**最后**，通过 `result.shift()` 把第一个坑去掉，就是我们的结果。

Submit 提交：

```js
Accepted
* 51/51 cases passed (324 ms)
* Your runtime beats 7.14 % of javascript submissions
* Your memory usage beats 13.33 % of javascript submissions (76.1 MB)
```

当然，为了代码的条理性，我们编写了一些无用代码，**jsliang** 整理下：

> 暴力破解【简化】

```js
const gardenNoAdj = (N, paths) => {
  // 1. 构造通道，索引 0 对应花园 1
  const gardenPath = Array.from(Array(N), () => []);
  
  // 2. 填充数据
  for (let i = 0; i < paths.length; i++) {
    gardenPath[paths[i][0] - 1].push(paths[i][1]);
    gardenPath[paths[i][1] - 1].push(paths[i][0]);
  }
  
  // 3. 开始挖坑，拿好花种
  const result = Array.from(Array(N), () => '');
  const flowers = [1, 2, 3, 4];

  // 4. 开始填坑
  for (let i = 0; i < gardenPath.length; i++) {
    const path = gardenPath[i].map(item => result[item - 1]);
    const canUse = Array.from(new Set([...flowers].filter(item => !path.includes(item))));
    result[i] = canUse[0];
  }

  // 5. 去掉没用的坑
  return result;
};
```

Submit 提交：

```js
Accepted
* 51/51 cases passed (240 ms)
* Your runtime beats 16.67 % of javascript submissions
* Your memory usage beats 16.67 % of javascript submissions (73.5 MB)
```

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

