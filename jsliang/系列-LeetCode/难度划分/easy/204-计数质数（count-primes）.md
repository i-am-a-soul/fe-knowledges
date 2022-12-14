204 - 计数质数（count-primes）
===

> Create by **jsliang** on **2019-07-10 19:07:34**  
> Recently revised in **2019-7-11 11:01:06**

## <a name="chapter-one" id="chapter-one">一 目录</a>

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 解题](#chapter-three) |
| [四 执行测试](#chapter-four) |
| [五 LeetCode Submit](#chapter-five) |
| [六 解题思路](#chapter-six) |
| [七 进一步思考](#chapter-seven) |
| [八 再进一步思考](#chapter-eight) |

## <a name="chapter-two" id="chapter-two">二 前言</a>



* **难度**：简单
* **涉及知识**：哈希表、数学
* **题目地址**：https://leetcode-cn.com/problems/count-primes/
* **题目内容**：

```
统计所有小于非负整数 n 的质数的数量。

示例:

输入: 10
输出: 4
解释: 小于 10 的质数一共有 4 个, 它们是 2, 3, 5, 7 。
```

## <a name="chapter-three" id="chapter-three">三 解题</a>



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **解题代码 - 厄拉多塞筛法**：

```js
var countPrimes = function (n) {
  if (n < 3) {
    return 0;
  }
  let result = [...new Array(n).keys()];
  result[0] = result[1] = null;
  for (let i = 2; i < n; i++) {
    for (let j = 2; i * j <= n; j++) {
      result[i * j] = null;
    }
  }
  result = result.filter(a => {
    return a != null;
  });
  return result.length;
};
```

## <a name="chapter-four" id="chapter-four">四 执行测试</a>



1. `n`：`10000`
2. `return`：`1229`

## <a name="chapter-five" id="chapter-five">五 LeetCode Submit</a>



```js
✔ Accepted
  ✔ 20/20 cases passed (344 ms)
  ✔ Your runtime beats 51.99 % of javascript submissions
  ✔ Your memory usage beats 11.65 % of javascript submissions (129.8 MB)
```

## <a name="chapter-six" id="chapter-six">六 解题思路</a>



**算法？数学？你会不会觉得智商往往不足了**~

**首先**，讲下什么是 **厄拉多塞筛法**：

西元前 250 年，希腊数学家厄拉多塞（Eeatosthese）想到了一个非常美妙的质数筛法，减少了逐一检查每个数的的步骤，可以比较简单的从一大堆数字之中，筛选出质数来，这方法被称作厄拉多塞筛法（Sieve of Eeatosthese）。

具体操作：

1. 先将 2~n 的各个数放入表中，然后在 2 的上面画一个圆圈，表示 2 是质数，然后划去 2 的其他倍数；
2. 接着，上一步中第 1 个既未画圈又没有被划去的数是 3，将它画圈，表示它是质数，再划去3的其他倍数；
3. 再来，现在既未画圈又没有被划去的第 1 个数是 5，将它画圈，表示它是质数，并划去 5 的其他倍数
4. ……依次类推，一直到所有小于或等于 n 的各数都画了圈或划去为止。这时，表中画了圈的以及未划去的那些数正好就是小于 n 的素数。

**然后**，我们查看大神操作：

```js
var countPrimes = function (n) {
  if (n < 3) {
    return 0;
  }
  let result = [...new Array(n).keys()];
  result[0] = result[1] = null;
  for (let i = 2; i < n; i++) {
    for (let j = 2; i * j <= n; j++) {
      result[i * j] = null;
      console.log(result);
    }
  }
  result = result.filter(a => {
    return a != null;
  });
  return result.length;
};
```

1. 生成一个数组，表示从 `0` 到 `n - 1`，就好比输入 `10`，返回的即是：`[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]`。
2. 然后设置 `0` 和 `1` 为 `null`，表明它两不参与筛选。
3. 循环遍历，`i` 即底数，`j` 为倍数，先画掉 `2` 的倍数，再画掉 `3` 的倍数，依次类推。（这里没处理好的是，它会循环到 `4`、`6` 等）
4. 双重 `for()` 遍历之后，现在只剩下 `null` 和质数，我们通过 `filter` 将 `null` 去掉。

> **jsliang** 在代码中埋了个 `console.log`，方便小伙伴们观察：

```js
[ null, null, 2, 3, null, 5, 6, 7, 8, 9 ]
[ null, null, 2, 3, null, 5, null, 7, 8, 9 ]
[ null, null, 2, 3, null, 5, null, 7, null, 9 ]
[ null, null, 2, 3, null, 5, null, 7, null, 9, null ]
[ null, null, 2, 3, null, 5, null, 7, null, 9, null ]
[ null, null, 2, 3, null, 5, null, 7, null, null, null ]
[ null, null, 2, 3, null, 5, null, 7, null, null, null ]
[ null, null, 2, 3, null, 5, null, 7, null, null, null ]
```

**最后**，统计剩下的长度，就是我们需要的结果值。

## <a name="chapter-seven" id="chapter-seven">七 进一步思考</a>



前面我们发现了一个问题，就是当我们的底数为 `4`、`6` 等数的时候，我们还会执行一遍 `for()` 循环，这样就有些浪费时间了，下面我们进行处理：

```js
var countPrimes = function (n) {
  if (n < 3) {
    return 0;
  }
  let result = [...new Array(n).keys()];
  result[0] = result[1] = null;
  for (let i = 2; i < n; i++) {
		if (result[i]) {
			for (let j = 2; i * j <= n; j++) {
				result[i * j] = null;
			}
		}
  }
  result = result.filter(a => {
    return a != null;
  });
  return result.length;
};
```

经过处理，效果是有的：

```js
√ Accepted
  √ 20/20 cases passed (244 ms)
  √ Your runtime beats 65.56 % of javascript submissions
  √ Your memory usage beats 11.65 % of javascript submissions (134.9 MB)
```

## <a name="chapter-eight" id="chapter-eight">八 再进一步思考</a>



经过大佬启发，想到自己能不能解出来呢？于是想到 **暴力破解**：

```js
var countPrimes = function (n) {
  if (n < 3) {
    return 0;
	}
	let length = 1;
	n = n - 1;
	while(n > 2) {
		for (let i = 2; i < n; i++) {
			if (n % i === 0) {
				break;
			} else if (i === n - 1 && n % i !== 0) {
				length++;
			}
		};
		n--;
	}
	return length;
};
```

当然，失败了：

```js
× Time Limit Exceeded
  × 17/20 cases passed (N/A)
  × testcase: '499979'
  × answer: 
  × expected_answer: 
  × stdout:
```

在测试用例 `17` 的时候就超时了，思路没错，只是耗费的时间太长了。

所以，小伙伴们有更好的方法，可以贴出来~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-small-wechat-public-address.jpg)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

扫描上方二维码，关注 **jsliang** 的公众号，让我们一起折腾！

