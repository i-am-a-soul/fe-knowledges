1299 - 将每个元素替换为右侧最大元素（replace-elements-with-greatest-element-on-right-side）
===

> Create by **jsliang** on **2020-02-01 19:05:34**  
> Recently revised in **2020-02-01 19:42:42**

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
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/replace-elements-with-greatest-element-on-right-side/
* **题目内容**：

```
给你一个数组 arr ，
请你将每个元素用它右边最大的元素替换，
如果是最后一个元素，用 -1 替换。

完成所有替换操作后，请你返回这个数组。

示例：

输入：arr = [17,18,5,4,6,1]
输出：[18,6,6,6,1,-1]

提示：

1 <= arr.length <= 10^4
1 <= arr[i] <= 10^5

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/replace-elements-with-greatest-element-on-right-side
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} arr
 * @return {number[]}
 */
var replaceElements = function(arr) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 将每个元素替换为右侧最大元素
 * @param {number[]} arr
 * @return {number[]}
 */
const replaceElements = (arr) => {
  const newArr = [...arr].sort((a, b) => b - a);
  for (let i = 0; i < arr.length; i++) {
    const index = newArr.indexOf(arr[i]);
    newArr.splice(index, 1);
    arr[i] = newArr[0];
  }
  arr[arr.length - 1] = -1;
  return arr;
};

console.log(replaceElements([17, 18, 5, 4, 6, 1])); // [ 18, 6, 6, 6, 1, -1 ]
```

`node index.js` 返回：

```js
[ 18, 6, 6, 6, 1, -1 ]
```

## 四 LeetCode Submit



```js
Accepted
* 15/15 cases passed (316 ms)
* Your runtime beats 32.42 % of javascript submissions
* Your memory usage beats 27.85 % of javascript submissions (41.1 MB)
```

## 五 解题思路



仔细思考了这道题，一开始想了个笨法子（太笨就不展示了），觉得可能会超时。

于是琢磨了下：

> 暴力破解

```js
const replaceElements = (arr) => {
  const newArr = [...arr].sort((a, b) => b - a);
  for (let i = 0; i < arr.length; i++) {
    const index = newArr.indexOf(arr[i]);
    newArr.splice(index, 1);
    arr[i] = newArr[0];
  }
  arr[arr.length - 1] = -1;
  return arr;
};
```

我们执行了以下步骤：

1. 先对 `newArr` 进行 `arr` 的从大到小倒序排序。
2. 遍历 `arr`，先查找 `newArr` 中 `arr[i]` 这个元素并删除。
3. 设置 `arr[i]` 为当前数组最大的元素（即 `arr[0]`）。
4. 最后特意设置最后一个元素为 `-1`，返回 `arr` 即可。

Submit 提交：

```js
Accepted
* 15/15 cases passed (316 ms)
* Your runtime beats 32.42 % of javascript submissions
* Your memory usage beats 27.85 % of javascript submissions (41.1 MB)
```

## 六 进一步思考



官方总能让我意想不到：

> 逆序遍历

```js
const replaceElements = (arr) => {
  const result = Array.from(Array(arr.length), () => '');
  result[result.length - 1] = -1;
  for (let i = arr.length - 2; i >= 0; i--) {
    result[i] = Math.max(result[i + 1], arr[i + 1]);
  }
  return result;
};
```

因为最后输出的数组是倒序的，所以我们通过倒序比较 `arr` 即可。

> 说，你的天地一号哪里买的！

Submit 提交：

```js
Accepted
* 15/15 cases passed (100 ms)
* Your runtime beats 68.49 % of javascript submissions
* Your memory usage beats 31.65 % of javascript submissions (40.3 MB)
```

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

