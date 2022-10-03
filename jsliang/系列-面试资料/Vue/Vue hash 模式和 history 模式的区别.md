Vue hash 模式和 history 模式的区别
===

> Create by **jsliang** on **2020-09-07 21:26:54**  
> Recently revised in **2020-09-07 21:30:04**

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- |
| [一 目录](#chapter-one) |
| [二 前言](#chapter-two) |

## 二 前言



1. 明显区别。`hash` 模式的 URL 夹杂 `#` 号，而 `history` 没有
2. 底层不同。`hash` 模式依靠 `onhashchange` 事件，监听 `location.hash` 的改变；而 `history` 模式主要是依靠 HTML5 history 新增的两个方法：`pushState()` 和 `repalceState()`，其中 `pushState()` 可以改变 `url` 地址且不会发送请求，`repalceState()` 可以读取历史记录栈，对浏览器记录进行修改。

---

