1047 - 删除字符串中的所有相邻重复项（remove-all-adjacent-duplicates-in-string）
===

> Create by **jsliang** on **2020-01-30 21:42:54**  
> Recently revised in **2020-01-30 22:17:59**

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
* **涉及知识**：栈
* **题目地址**：https://leetcode-cn.com/problems/remove-all-adjacent-duplicates-in-string/
* **题目内容**：

```
给出由小写字母组成的字符串 S，
重复项删除操作会选择两个相邻且相同的字母，
并删除它们。

在 S 上反复执行重复项删除操作，
直到无法继续删除。

在完成所有重复项删除操作后返回最终的字符串。
答案保证唯一。 

示例：

输入："abbaca"
输出："ca"
解释：
例如，在 "abbaca" 中，
我们可以删除 "bb" 由于两字母相邻且相同，
这是此时唯一可以执行删除操作的重复项。
之后我们得到字符串 "aaca"，
其中又只有 "aa" 可以执行重复项删除操作，
所以最后的字符串为 "ca"。

提示：

1 <= S.length <= 20000
S 仅由小写英文字母组成。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/remove-all-adjacent-duplicates-in-string
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} S
 * @return {string}
 */
var removeDuplicates = function(S) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 删除字符串中的所有相邻重复项
 * @param {string} S
 * @return {string}
 */
const removeDuplicates = (S) => {
  const stack = [];
  for (let i = 0; i < S.length; i++) {
    if (stack[stack.length - 1] === S[i]) {
      stack.pop();
    } else {
      stack.push(S[i]);
    }
  }
  return stack.join('');
};

console.log(removeDuplicates('abbaca')); // 'ca'
console.log(removeDuplicates('aababaab')); // 'ba'
```

`node index.js` 返回：

```js
ca
```

## 四 LeetCode Submit



```js
Accepted
* 98/98 cases passed (88 ms)
* Your runtime beats 73.64 % of javascript submissions
* Your memory usage beats 23.79 % of javascript submissions (42.5 MB)
```

## 五 解题思路



开心消消乐又来咯：

1. 有一串字符 `abbaca`，如果它当中有两个连在一起的，就消掉，直到不能再消为止。
2. 消除的过程： `abbaca` => `aaca` => `ca`。

好，直到规则，开始搞事：

> 暴力破解

```js
const removeDuplicates = (S) => {
  let newS = '';
  let flag = false;
  while (!flag) {
    let remove = false;
    for (let i = 0; i < S.length; i++) {
      if (S[i] === S[i + 1]) {
        i++;
        remove = true;
      } else {
        newS += S[i];
      }
    }
    S = newS;
    if (!remove) {
      flag = true;
    } else {
      remove = false;
      newS = '';
    }
  }
  return newS;
};
```

解析：

1. 设置 `newS` 来获取当前消除后的字符串。
2. 设置 `flag` 来判断是否中止开心消消乐。
3. 通过 `for` 遍历 S，判断是否存在 `S[i] === S[i + 1]`，如果存在，则跳两格，不添加这两个相同的，同时表明 `remove = true`，表明我消除过。
4. 循环结束后，将 `S` 替换为 `newS` 的内容，以示接下来如果还需要消除的话，就进一步消除。
5. 同时，判断这次是否进行了 `remove`，如果没进行，那就是最终结果；如果消除了，那么清空 `newS` 和重置 `remove`，卷土重来~

Submit 提交：

```js
Accepted
* 98/98 cases passed (100 ms)
* Your runtime beats 41.82 % of javascript submissions
* Your memory usage beats 65.64 % of javascript submissions (42 MB)
```

那么，是否存在一次遍历，就可以全部消除的方法？

> 线性遍历

```js
const removeDuplicates = (S) => {
  const stack = [];
  for (let i = 0; i < S.length; i++) {
    if (stack[stack.length - 1] === S[i]) {
      stack.pop();
    } else {
      stack.push(S[i]);
    }
  }
  return stack.join('');
};
```

这道题和判断有效的括号很想象，直接判断栈顶的内容即可~

Submit 提交：

```js
Accepted
* 98/98 cases passed (88 ms)
* Your runtime beats 73.64 % of javascript submissions
* Your memory usage beats 23.79 % of javascript submissions (42.5 MB)
```

当然，除此之外，还有一种方法，就是官方题解中的，使用正则替换出现的 `['aa', 'bb', 'cc', ..., 'zz']` 重复项，然后循环替换即可（跟 **jsliang** 暴力相似）：

* https://leetcode-cn.com/problems/remove-all-adjacent-duplicates-in-string/solution/shan-chu-zi-fu-chuan-zhong-de-suo-you-xiang-lin-zh/

这里咱就不多逼逼了，感兴趣的小伙伴可以去看看。

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

