Map
===

> Create by **jsliang** on **2019-09-16 15:41:07**  
> Recently revised in **2019-09-18 08:50:26**

* **原文**：[MDN - Map](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map)

* **功能**：`Map` 对象保存键值对。

* **方法**：
  * `new Map()`：新建一个 `Map` 对象
  * `Map.prototype.has(key)`：返回布尔值。表示 Map 实例是否包含键对应的值。
  * `Map.prototype.set(key, value)`：返回该 Map 对象。设置 Map 对象中键的值。
  * `Map.prototype.get(key)`：返回键对应的值，如果不存在，则返回 undefined。
  * `Map.prototype.delete(key)`：如果 Map 对象中存在该元素，则移除它并返回 `true`；否则如果该元素不存在则返回 `false`。

* **代码**：

```js
var twoSum = function(nums, target) {
  let map = new Map();
  for (let i = 0; i < nums.length; i++) {
    if (map.has(nums[i])) {
      return [map.get(nums[i]), i];
    } else {
      map.set(target - nums[i], i);
    }
  }
};

twoSum([4, 3, 2, 5, 6], 8); // [1, 3]
```

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

