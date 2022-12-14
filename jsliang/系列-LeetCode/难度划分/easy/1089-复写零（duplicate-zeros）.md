1089 - 复写零（duplicate-zeros）
===

> Create by **jsliang** on **2020-01-31 12:00:11**  
> Recently revised in **2020-01-31 12:13:13**

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
* **题目地址**：https://leetcode-cn.com/problems/duplicate-zeros/
* **题目内容**：

```
给你一个长度固定的整数数组 arr，
请你将该数组中出现的每个零都复写一遍，
并将其余的元素向右平移。

注意：请不要在超过该数组长度的位置写入元素。

要求：请对输入的数组 就地 进行上述修改，不要从函数返回任何东西。

示例 1：

输入：[1,0,2,3,0,4,5,0]
输出：null
解释：调用函数后，输入的数组将被修改为：[1,0,0,2,3,0,0,4]
示例 2：

输入：[1,2,3]
输出：null
解释：调用函数后，输入的数组将被修改为：[1,2,3]

提示：

1 <= arr.length <= 10000
0 <= arr[i] <= 9

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/duplicate-zeros
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} arr
 * @return {void} Do not return anything, modify arr in-place instead.
 */
var duplicateZeros = function(arr) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 复写零
 * @param {number[]} arr
 * @return {void} Do not return anything, modify arr in-place instead.
 */
const duplicateZeros = (arr) => {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === 0) {
      arr.splice(i + 1, 0, 0);
      arr.pop();
      i++;
    }
  }
};

console.log(duplicateZeros([1, 0, 2, 3, 0, 4, 5, 0])); // [ 1, 0, 0, 2, 3, 0, 0, 4 ]
```

`node index.js` 返回：

```js
[ 1, 0, 0, 2, 3, 0, 0, 4 ]
```

## 四 LeetCode Submit



```js
Accepted
* 30/30 cases passed (84 ms)
* Your runtime beats 75.36 % of javascript submissions
* Your memory usage beats 31.82 % of javascript submissions (35.6 MB)
```

## 五 解题思路



题意很简单：

* 给定一个数组：[0, 1, 2]，然后将数组中存在的所有 0 复制一个，最后变成 `[0, 0, 1]`。

注意：数组长度不变，需要原地修改数组。

那没什么好说的，直接上代码：

> 暴力破解

```js
const duplicateZeros = (arr) => {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === 0) {
      arr.splice(i + 1, 0, 0);
      arr.pop();
      i++;
    }
  }
};
```

如果这个数为 0，那么往它后面删除 0 个元素，插入 1 个 0。

> 注意：`splice(index, deleteItem, addItem)`

接着将数组末尾元素推出，保持数组长度不变。

最后就是 `i++`，毕竟下一个元素是我们添加的~

Submit 提交：

```js
Accepted
* 30/30 cases passed (84 ms)
* Your runtime beats 75.36 % of javascript submissions
* Your memory usage beats 31.82 % of javascript submissions (35.6 MB)
```

## 六 进一步思考



【题解区】和【评论区】有双指针、快慢指针等方法~

这里就不一一吐槽啦，毕竟有兴趣的小伙伴可以直接探索。

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

