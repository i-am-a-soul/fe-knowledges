1108 - IP地址无效化（defanging-an-ip-address）
===

> Create by **jsliang** on **2020-01-31 12:37:17**  
> Recently revised in **2020-01-31 13:19:51**

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
* **涉及知识**：字符串
* **题目地址**：https://leetcode-cn.com/problems/defanging-an-ip-address/
* **题目内容**：

```
给你一个有效的 IPv4 地址 address，
返回这个 IP 地址的无效化版本。

所谓无效化 IP 地址，
其实就是用 "[.]" 代替了每个 "."。

示例 1：

输入：address = "1.1.1.1"
输出："1[.]1[.]1[.]1"

示例 2：

输入：address = "255.100.50.0"
输出："255[.]100[.]50[.]0"

提示：

给出的 address 是一个有效的 IPv4 地址

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/defanging-an-ip-address
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} address
 * @return {string}
 */
var defangIPaddr = function(address) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name IP地址无效化
 * @param {string} address
 * @return {string}
 */
const defangIPaddr = (address) => {
  return address.split('').map(item => item === '.' ? `[.]` : item).join('');
};

console.log(defangIPaddr('1.1.1.1')); // 1[.]1[.]1[.]1
```

`node index.js` 返回：

```js
1[.]1[.]1[.]1
```

## 四 LeetCode Submit



```js
Accepted
* 62/62 cases passed (60 ms)
* Your runtime beats 81.63 % of javascript submissions
* Your memory usage beats 30.27 % of javascript submissions (33.8 MB)
```

## 五 解题思路



首先，需要知道的是，JavaScript 毕竟非常灵活：

> 【Plan A】一行求解

```js
const defangIPaddr = (address) => address.split('').map(item => item === '.' ? `[.]` : item).join('');
```

Submit 提交：

```js
Accepted
* 62/62 cases passed (60 ms)
* Your runtime beats 81.63 % of javascript submissions
* Your memory usage beats 30.27 % of javascript submissions (33.8 MB)
```

> 【Plan B】两行求解

```js
const defangIPaddr = (address) => {
  return address.split('').reduce((prev, next) => {
    return next === '.' ? prev + '[.]' : prev + next;
  });
};
```

Submit 提交：

```js
Accepted
* 62/62 cases passed (92 ms)
* Your runtime beats 6.69 % of javascript submissions
* Your memory usage beats 29.4 % of javascript submissions (33.8 MB)
```

> 【Plan C】正常求解

```js
const defangIPaddr = (address) => {
  let result = '';
  for (let i = 0; i < address.length; i++) {
    if (address[i] === '.') {
      result += '[.]';
    } else {
      result += address[i];
    }
  }
  return result;
};
```

Submit 提交：

```js
Accepted
* 62/62 cases passed (60 ms)
* Your runtime beats 81.63 % of javascript submissions
* Your memory usage beats 41.31 % of javascript submissions (33.8 MB)
```

小伙伴喜欢哪款随意拿去，更多的 **jsliang** 就不多逼逼了。

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

