Object.defineProperty 和 Proxy
===

> Create by **jsliang** on **2020-04-24 11:19:51**  
> Recently revised in **2020-09-29 08:52:51**

**欢迎关注 jsliang 的文档库 —— 一个穷尽一生更新的仓库，查看更多技术、理财、健身文章：https://github.com/LiangJunrong/document-library**

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 实战](#chapter-three) |
| [四 参考文献](#chapter-four) |
| [五 个人整理](#chapter-five) |
| &emsp;[5.1 区别](#chapter-five-one) |
| [六 总结](#chapter-six) |

## 二 前言



上周在学习过程中，接触到了 `Object.defineProperty` 和 `Proxy` 来构建 MVVM，对此感到有点兴趣，陆续也看到一些两者对比的文章，在此进行总结比对。

## 三 实战



* 项目地址：https://github.com/LiangJunrong/all-for-one
* 项目位置：011 —— 013（没基础的小伙伴可以从 009 看起）
* 代码

> Object.defineProperty

```js
observer(data) {
  const dep = new Dep();
  for (let key in data) {
    let value = data[key];
    Object.defineProperty(data, key, {
      configurable: true,
      enumerable: true,
      get() {
        if (Dep.target) {
          dep.addSub(Dep.target);
        }
        return value;
      },
      set(newValue) {
        dep.notify(newValue, key);
        if (newValue !== value) {
          value = newValue;
        }
      }
    });
  }
};

// 绑定事件二次渲染视图
for (let i = 0; i < result.length; i++) {
  new Watcher(this._data, result[i], (newValue, key) => {
    if (result[i] === key) {
      textContent = textContent.replace(this._data[result[i]], newValue);
    }
    node.textContent = textContent;
  });
}
```

> Proxy

```js
observer(data) {
  const dep = new Dep();
  this._data = new Proxy(data, {
    get(target, key) {
      if (Dep.target) {
        dep.addSub(Dep.target);
      }
      return target[key];
    },
    set(target, key, newValue) {
      dep.notify(newValue, key);
      target[key] = newValue;
      return true;
    }
  })
};

// 绑定事件二次渲染视图
for (let i = 0; i < result.length; i++) {
  new Watcher(this._data, result[i], (newValue, key) => {
    if (result[i] === key) {
      textContent = textContent.replace(this._data[result[i]], newValue);
    }
    node.textContent = textContent;
  });
}
```

> 发布订阅

```js
// 发布订阅
// 发布者
class Dep {
  constructor() {
    this.subs = [];
  };
  addSub(sub) {
    this.subs.push(sub);
  };
  // 发布
  notify(newValue, key) {
    this.subs.forEach((sub) => {
      sub.update(newValue, key);
    });
  }
}
// 订阅者
class Watcher {
  constructor(data, key, cb) {
    Dep.target = this;
    this.cb = cb;
    // 人为触发 get
    data[key];
    Dep.target = null;
  };
  update(newValue, key) {
    this.cb(newValue, key);
  }
}
```

将 `Object.defineProperty` 升级到 `Proxy` 是很顺滑的，更新的代码并不多，但是课程讲师说这个 `Proxy` 具备很大优势，有多大呢？咱一起看看。

## 四 参考文献



* [【掘金】晨曦时梦见兮《Vue3 的响应式和以前有什么区别，Proxy 无敌？》](https://juejin.im/post/5e92d863f265da47e57fe065)

## 五 个人整理



### 5.1 区别



`Proxy` 和 `Object.defineProperty` 的使用方法看似很相似，其实 `Proxy` 是在 「更高维度」 上去拦截属性的修改的，怎么理解呢？

Vue2 中，对于给定的 `data`，如 `{ count: 1 }`，是需要根据具体的 `key` 也就是 `count`，去对「修改 data.count 」 和 「读取 data.count」进行拦截，也就是

```js
Object.defineProperty(data, 'count', {
  get() {},
  set() {},
})
```

复制代码必须预先知道要拦截的 `key` 是什么，这也就是为什么 Vue2 里对于对象上的新增属性无能为力。

而 Vue3 所使用的 `Proxy`，则是这样拦截的：

```js
new Proxy(data, {
  get(key) { },
  set(key, value) { },
})
```

复制代码可以看到，根本不需要关心具体的 `key`，它去拦截的是 「修改 data 上的任意 key」 和 「读取 data 上的任意 key」。

所以，不管是已有的 `key`  还是新增的 `key`，都逃不过它的魔爪。

但是 `Proxy` 更加强大的地方还在于 `Proxy` 除了 `get` 和 `set`，还可以拦截更多的操作符。

```
* 作者：晨曦时梦见兮
* 链接：https://juejin.im/post/5e92d863f265da47e57fe065
* 来源：掘金
* 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

## 六 总结



--

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

