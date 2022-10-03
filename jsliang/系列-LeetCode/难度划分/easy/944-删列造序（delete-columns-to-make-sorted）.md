944 - 删列造序（delete-columns-to-make-sorted）
===

> Create by **jsliang** on **2020-01-27 19:31:53**  
> Recently revised in **2020-01-27 20:13:58**

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
* **涉及知识**：贪心算法
* **题目地址**：https://leetcode-cn.com/problems/delete-columns-to-make-sorted/
* **题目内容**：

```
给定由 N 个小写字母字符串组成的数组 A，
其中每个字符串长度相等。

删除 操作的定义是：选出一组要删掉的列，
删去 A 中对应列中的所有字符，
形式上，第 n 列为 [A[0][n], A[1][n],
..., A[A.length-1][n]]）。

比如，有 A = ["abcdef", "uvwxyz"]，

| a | b | c | d | e | f |
| u | v | w | x | y | z |

要删掉的列为 {0, 2, 3}，
删除后 A 为["bef", "vyz"]，
A 的列分别为["b","v"], ["e","y"], ["f","z"]。

| b | e | f |
| v | y | z |

你需要选出一组要删掉的列 D，
对 A 执行删除操作，
使 A 中剩余的每一列都是 非降序 排列的，
然后请你返回 D.length 的最小可能值。

示例 1：

输入：["cba", "daf", "ghi"]
输出：1
解释：
当选择 D = {1}，
删除后 A 的列为：["c","d","g"] 和 ["a","f","i"]，
均为非降序排列。
若选择 D = {}，
那么 A 的列 ["b","a","h"] 就不是非降序排列了。

示例 2：

输入：["a", "b"]
输出：0
解释：D = {}

示例 3：

输入：["zyx", "wvu", "tsr"]
输出：3
解释：D = {0, 1, 2}

提示：

1 <= A.length <= 100
1 <= A[i].length <= 1000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/delete-columns-to-make-sorted
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string[]} A
 * @return {number}
 */
var minDeletionSize = function(A) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 删列造序
 * @param {string[]} A
 * @return {number}
 */
const minDeletionSize = (A) => {
  let result = 0;
  for (let i = 0; i < A[0].length; i++) {
    for (let j = 0; j < A.length - 1; j++) {
      if (A[j][i] > A[j + 1][i]) {
        result ++;
        break;
      }
    }
  }
  return result;
};

console.log(minDeletionSize(['cba', 'daf', 'ghi'])); // 1
console.log(minDeletionSize(['a', 'b'])); // 0
console.log(minDeletionSize(['zyx', 'wvu', 'tsr'])); // 3
```

`node index.js` 返回：

```js
1
0
3
```

## 四 LeetCode Submit



```js
Accepted
* 84/84 cases passed (1368 ms)
* Your runtime beats 5.51 % of javascript submissions
* Your memory usage beats 5.45 % of javascript submissions (68.2 MB)
```

## 五 解题思路



明白题意：

1. 你需要知道啥叫删除列（看题目）
2. 你需要选出一组要删掉的列 D，对 A 执行删除操作，使 A 中剩余的每一列都是 非降序 排列的（即升序），然后请你返回 `D.length` 的最小可能值。

> 暴力破解

```js
const minDeletionSize = (A) => {
  // 1. 重置新数组
  const resetArray = Array.from(Array(A[0].length), () => '');
  // 2. 按列重排数组
  for (let i = 0; i < A[0].length; i++) {
    for (let j = 0; j < A.length; j++) {
      resetArray[i] += A[j][i];
    }
  }
  // 3. 判断是否存在不为顺序的字符串
  let result = 0;
  for (let i = 0; i < resetArray.length; i++) {
    if (resetArray[i] !== resetArray[i].split('').sort((a, b) => a.localeCompare(b)).join('')) {
      result += 1;
    }
  }
  // 4. 返回结果
  return result;
};
```

Submit 提交如下：

```js
Accepted
* 84/84 cases passed (1368 ms)
* Your runtime beats 5.51 % of javascript submissions
* Your memory usage beats 5.45 % of javascript submissions (68.2 MB)
```

当然，如果你嫌弃上面看起来冗余，**jsliang** 为你压缩一下：

> 暴力破解【简化版】

```js
const minDeletionSize = (A) => {
  let result = 0;
  for (let i = 0; i < A[0].length; i++) {
    let tempArr = '';
    for (let j = 0; j < A.length; j++) {
      tempArr += A[j][i];
    }
    if (tempArr !== tempArr.split('').sort((a, b) => a.localeCompare(b)).join('')) {
      result += 1;
    }
  }
  return result;
};
```

Submit 提交如下：

```js
Accepted
* 84/84 cases passed (1692 ms)
* Your runtime beats 5.51 % of javascript submissions
* Your memory usage beats 10.91 % of javascript submissions (40.8 MB)
```

进入思考，效率还是那么低下，是我有什么没有考虑到么？

## 六 进一步思考



带着疑惑，咱们翻开【题解区】和【评论区】：

> 贪心算法

```js
const minDeletionSize = (A) => {
  let result = 0;
  for (let i = 0; i < A[0].length; i++) {
    for (let j = 0; j < A.length - 1; j++) {
      if (A[j][i] > A[j + 1][i]) {
        result ++;
        break;
      }
    }
  }
  return result;
};
```

精妙，直接在遍历的时候进行比对，如果下一个元素比当前元素小，那么说明它不是升序排列的~

Submit 提交：

```js
Accepted
* 84/84 cases passed (80 ms)
* Your runtime beats 90.55 % of javascript submissions
* Your memory usage beats 67.27 % of javascript submissions (39.4 MB)
```

近乎完美~

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

