1185 - 一周中的第几天（day-of-the-week）
===

> Create by **jsliang** on **2020-01-31 19:38:14**  
> Recently revised in **2020-01-31 20:32:54**

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
* **题目地址**：https://leetcode-cn.com/problems/day-of-the-week/
* **题目内容**：

```
给你一个日期，请你设计一个算法来判断它是对应一周中的哪一天。

输入为三个整数：day、month 和 year，分别表示日、月、年。

您返回的结果必须是这几个值中的一个
{
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday"
}。

示例 1：

输入：day = 31, month = 8, year = 2019
输出："Saturday"

示例 2：

输入：day = 18, month = 7, year = 1999
输出："Sunday"

示例 3：

输入：day = 15, month = 8, year = 1993
输出："Sunday"

提示：

给出的日期一定是在 1971 到 2100 年之间的有效日期。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/day-of-the-week
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 三 解题及测试



小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} day
 * @param {number} month
 * @param {number} year
 * @return {string}
 */
var dayOfTheWeek = function(day, month, year) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 一周中的第几天
 * @param {number} day
 * @param {number} month
 * @param {number} year
 * @return {string}
 */
const dayOfTheWeek = (day, month, year) => {
  if (month === 1 || month === 2) {
    month += 12;
    year -= 1;
  }
  const result = (day + 1 + 2 * month + Math.floor(3 * (month + 1) / 5) + year + Math.floor(year / 4) - Math.floor(year / 100) + Math.floor(year / 400)) % 7;
  return ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'][result];
};

console.log(dayOfTheWeek(31, 1, 2020)); // 'Firday'
console.log(dayOfTheWeek(18, 7, 1999)); // 'Sunday'
```

`node index.js` 返回：

```js
'Firday'
'Sunday'
```

## 四 LeetCode Submit



```js
Accepted
* 39/39 cases passed (64 ms)
* Your runtime beats 59.11 % of javascript submissions
* Your memory usage beats 76.88 % of javascript submissions (33.8 MB)
```

## 五 解题思路



众所周知，**jsliang** 在题目《1154-一年中的第几天》放了水，直接讲解了别人的答案。

没想到天道有轮回，一下子又要求《一周中的第几天》了，咱们试试吧：

> 暴力破解

```js
const dayOfTheWeek = (day, month, year) => {
  if (month === 1 || month === 2) {
    month += 12;
    year -= 1;
  }
  const result = (day + 1 + 2 * month + Math.floor(3 * (month + 1) / 5) + year + Math.floor(year / 4) - Math.floor(year / 100) + Math.floor(year / 400)) % 7;
  return ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'][result];
};
```

罪过罪过，网上找到公式直接套用~

Submit 提交：

```js
Accepted
* 39/39 cases passed (64 ms)
* Your runtime beats 59.11 % of javascript submissions
* Your memory usage beats 76.88 % of javascript submissions (33.8 MB)
```

## 六 进一步思考



在【题解区】和【评论区】，除了套公式的，还有套 JavaScript 原生 API 的：

> 使用 API

```js
const dayOfTheWeek = (day, month, year) => {
  const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
  let x = `${year}/${month}/${day}`;
  let date = new Date(Date.parse(x));
  return days[date.getDay()];
};
```

Submit 提交：

```js
Accepted
* 39/39 cases passed (52 ms)
* Your runtime beats 95.57 % of javascript submissions
* Your memory usage beats 35.63 % of javascript submissions (34.1 MB)
```

搞定，收工。

那么这道题就写到这里啦~

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

