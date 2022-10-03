1287 - 有序数组中出现次数超过25%的元素（element-appearing-more-than-25-in-sorted-array）
===

> Create by **jsliang** on **2020-02-01 17:58:22**  
> Recently revised in **2020-02-01 18:08:48**

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
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/element-appearing-more-than-25-in-sorted-array/
* **题目内容**：

```
给你一个非递减的 有序 整数数组，
已知这个数组中恰好有一个整数，
它的出现次数超过数组元素总数的 25%。

请你找到并返回这个整数

示例：

输入：arr = [1,2,2,6,6,6,6,7,10]
输出：6
 

提示：

1 <= arr.length <= 10^4
0 <= arr[i] <= 10^5

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/element-appearing-more-than-25-in-sorted-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} arr
 * @return {number}
 */
var findSpecialInteger = function(arr) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 有序数组中出现次数超过25%的元素
 * @param {number[]} arr
 * @return {number}
 */
const findSpecialInteger = (arr) => {
  let maxNumber = arr[0],
      maxTime = 1,
      nowNumber = arr[0],
      nowTime = 1;
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] === nowNumber) {
      nowTime++;
      if (nowTime > maxTime) {
        maxTime = nowTime;
        maxNumber = nowNumber;
      }
    } else {
      nowNumber = arr[i];
      nowTime = 1;
    }
  }
  return maxNumber;
};

console.log(findSpecialInteger([1, 2, 2, 6, 6, 6, 6, 7, 10])); // 6
```

`node index.js` 返回：

```js
6
```

## 四 LeetCode Submit



```js
Accepted
* 18/18 cases passed (68 ms)
* Your runtime beats 81.25 % of javascript submissions
* Your memory usage beats 84.04 % of javascript submissions (35.3 MB)
```

## 五 解题思路



**首先**，看完题目，难免怀疑下，会不会有多个元素超过 25%。

然后题目意思是：

```
给你一个非递减的 有序 整数数组，
已知这个数组中恰好有一个整数，
它的出现次数超过数组元素总数的 25%。
```

OK，那就假定：

1. 只有一个
2. 递增整数数组
3. 超过 25%

那么，开始解题：

> 暴力破解

```js
const findSpecialInteger = (arr) => {
  let maxNumber = arr[0],
      maxTime = 1,
      nowNumber = arr[0],
      nowTime = 1;
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] === nowNumber) {
      nowTime++;
      if (nowTime > maxTime) {
        maxTime = nowTime;
        maxNumber = nowNumber;
      }
    } else {
      nowNumber = arr[i];
      nowTime = 1;
    }
  }
  return maxNumber;
};
```

Submit 提交：

```js
Accepted
* 18/18 cases passed (68 ms)
* Your runtime beats 81.25 % of javascript submissions
* Your memory usage beats 84.04 % of javascript submissions (35.3 MB)
```

enm...这和前一道题《1281 - 整数的各位积和之差》一样，感觉都是入门级别的。

所以这里就不多 bb 啦~

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

