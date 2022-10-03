[toc]

# Vue

## vue 的响应式原理

数据发生变化后，会重新对页面渲染，这就是 Vue 响应式

想完成这个过程，我们需要：

- 侦测数据的变化
- 收集视图依赖了哪些数据
- 数据变化时，自动“通知”需要更新的视图部分，并进行更新

对应专业俗语分别是：

数据劫持 / 数据代理
依赖收集
发布订阅模式

## vue 双向数据绑定原理

> vue 通过使用双向数据绑定，来实现了 View 和 Model 的同步更新。vue 的双向数据绑定主要是通过使用数据劫持和发布订阅者模式来实现的。
>
> 首先我们通过 Object.defineProperty() 方法来对 Model 数据各个属性添加访问器属性，以此来实现数据的劫持，因此当 Model 中的数据发生变化的时候，我们可以通过配置的 setter 和 getter 方法来实现对 View 层数据更新的通知。
>
> 数据在 html 模板中一共有两种绑定情况，一种是使用 v-model 来对 value 值进行绑定，一种是作为文本绑定，在对模板引擎进行解析的过程中。
>
> 如果遇到元素节点，并且属性值包含 v-model 的话，我们就从 Model 中去获取 v-model 所对应的属性的值，并赋值给元素的 value 值。然后给这个元素设置一个监听事件，当 View 中元素的数据发生变化的时候触发该事件，通知 Model 中的对应的属性的值进行更新。
>
> 如果遇到了绑定的文本节点，我们使用 Model 中对应的属性的值来替换这个文本。对于文本节点的更新，我们使用了发布订阅者模式，属性作为一个主题，我们为这个节点设置一个订阅者对象，将这个订阅者对象加入这个属性主题的订阅者列表中。当 Model 层数据发生改变的时候，Model 作为发布者向主题发出通知，主题收到通知再向它的所有订阅者推送，订阅者收到通知后更改自己的数据。

## 使用 Object.defineProperty() 来进行数据劫持有什么缺点

有一些对属性的操作，使用这种方法无法拦截，比如说通过下标方式修改数组数据或者给对象新增属性，vue 内部通过重写函数解决了这个问题。

在 Vue3.0 中已经不使用这种方式了，而是通过使用 Proxy 对对象进行代理，从而实现数据劫持。使用 Proxy 的好处是它可以完美的监听到任何方式的数据改变，唯一的缺点是兼容性的问题，因为这是 ES6 的语法。

## vue 的 activated 和 deactivated 钩子函数

```html
<keep-alive>
  <component :is="view"></component>
</keep-alive>
```

`keep-alive`包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。

当组件在 `<keep-alive>` 内被切换，它的 `activated` 和 `deactivated` 这两个生命周期钩子函数将会被对应执行。

- `activated`在`keep-alive`组件激活时调用，该钩子函数在服务器端渲染期间不被调用。
- `deactivated`在`keep-alive`组件停用时调用，该钩子函数在服务端渲染期间不被调用。

## Vue中父子组件生命周期执行顺序

在单一组件中，钩子的执行顺序是beforeCreate-> created -> mounted->... ->destroyed

父子组件生命周期执行顺序：

- 加载渲染过程

  ```txt
  父beforeCreate->父created->父beforeMount->子beforeCreate->子created->子beforeMount->子mounted->父mounted
  ```

- 更新过程

  ```txt
  父beforeUpdate->子beforeUpdate->子updated->父updated
  ```

- 销毁过程

  ```txt
  父beforeDestroy->子beforeDestroy->子destroyed->父destroyed
  ```

- 常用钩子简易版

  ```txt
  父create->子created->子mounted->父mounted
  ```

## vue中key属性的作用

一句话 key 的作用主要是为了高效的更新虚拟 DOM

key 的特殊 attribute 主要用在 Vue 的虚拟 DOM 算法，在新旧 nodes 对比时辨识 VNodes。如果不使用 key，Vue 会使用一种最大限度减少动态元素并且尽可能的尝试就地修改/复用相同类型元素的算法。而使用 key 时，它会基于 key 的变化重新排列元素顺序，并且会移除 key 不存在的元素。

有相同父元素的子元素必须有独特的 key。重复的 key 会造成渲染错误。

## Vue中key属性用index为什么不行

这是由于diff算法的机制所决定的，话不多说，直接上反例：

当我们选中某一个（比如第3个），再添加或删除内容的时候就能发现bug了

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

</head>
<body>
    <div id="app">
        <span>ID:</span><input type="text" v-model="id">
        <span>Name:</span><input type="text" v-model="name">
        <button @click="handleClick">添加</button>

        <div v-for="(item, index) in list" :key="index">
            <input type="checkbox" />
            <span @click="handleDelete(index)">{{item.id}} --- {{item.name}}</span>
        </div>
    </div>
    <script>
        let vm = new Vue({
            el: '#app',
            data: {
                id: '',
                name: '',
                list: [
                    {id: 1, name: '张三'},
                    {id: 2, name: '李四'},
                    {id: 3, name: '王五'},
                    {id: 4, name: '赵六'},
                ]
            },
            methods: {
                handleClick() {
                    this.list.unshift({
                        id: this.id,
                        name: this.name
                    })
                },
                handleDelete(index) {
                    this.list.splice(index, 1)
                }
            },
        })
    </script>
</body>
</html>

```

## Vue diff算法详解

- updateChildren

> 这个函数是用来比较两个结点的子节点

```js
updateChildren(parentElm, oldCh, newCh) {
    let oldStartIdx = 0,
        newStartIdx = 0
    let oldEndIdx = oldCh.length - 1
    let oldStartVnode = oldCh[0]
    let oldEndVnode = oldCh[oldEndIdx]
    let newEndIdx = newCh.length - 1
    let newStartVnode = newCh[0]
    let newEndVnode = newCh[newEndIdx]
    let oldKeyToIdx
    let idxInOld
    let elmToMove
    let before
    while (oldStartIdx <= oldEndIdx && newStartIdx <= newEndIdx) { // 只有 oldS>oldE 或者 newS>newE 才会终止循环
        if (oldStartVnode == null) { // 对于vnode.key的比较，会把oldVnode = null
            oldStartVnode = oldCh[++oldStartIdx]
        } else if (oldEndVnode == null) {
            oldEndVnode = oldCh[--oldEndIdx]
        } else if (newStartVnode == null) {
            newStartVnode = newCh[++newStartIdx]
        } else if (newEndVnode == null) { // 到这里是找到第一个不为null的oldStartVnode oldEndVnode newStartVnode newEndVnode
            newEndVnode = newCh[--newEndIdx]
        } else if (sameVnode(oldStartVnode, newStartVnode)) { // oldS指针和newS指针对应的结点相同时，将oldS和newS指针同时向后移一位
            patchVnode(oldStartVnode, newStartVnode)
            oldStartVnode = oldCh[++oldStartIdx]
            newStartVnode = newCh[++newStartIdx]
        } else if (sameVnode(oldEndVnode, newEndVnode)) { // oldE指针和newE指针对应的结点相同时，将oldE和newE指针同时向前移一位
            patchVnode(oldEndVnode, newEndVnode)
            oldEndVnode = oldCh[--oldEndIdx]
            newEndVnode = newCh[--newEndIdx]
        } else if (sameVnode(oldStartVnode, newEndVnode)) { // oldS指针和newE指针对应的结点相同时，将oldS指针对应结点移动到oldE指针之后，同时将oldS指针向后移动一位，newE指针向前移动一位
            patchVnode(oldStartVnode, newEndVnode)
            api.insertBefore(parentElm, oldStartVnode.el, api.nextSibling(oldEndVnode.el))
            oldStartVnode = oldCh[++oldStartIdx]
            newEndVnode = newCh[--newEndIdx]
        } else if (sameVnode(oldEndVnode, newStartVnode)) { // oldE指针和newS指针对应的结点相同时，将oldE指针对应的结点移动到oldS指针之前，同时将oldE指针向前移动一位，newS指针想后移动一位
            patchVnode(oldEndVnode, newStartVnode)
            api.insertBefore(parentElm, oldEndVnode.el, oldStartVnode.el)
            oldEndVnode = oldCh[--oldEndIdx]
            newStartVnode = newCh[++newStartIdx]
        } else { // 使用key时的比较
            if (oldKeyToIdx === undefined) {
                oldKeyToIdx = createKeyToOldIdx(oldCh, oldStartIdx, oldEndIdx) // 有key生成index表
            }
            idxInOld = oldKeyToIdx[newStartVnode.key]
            if (!idxInOld) {
                api.insertBefore(parentElm, createEle(newStartVnode).el, oldStartVnode.el)
                newStartVnode = newCh[++newStartIdx]
            } else {
                elmToMove = oldCh[idxInOld]
                if (elmToMove.sel !== newStartVnode.sel) {
                    api.insertBefore(parentElm, createEle(newStartVnode).el, oldStartVnode.el)
                } else {
                    patchVnode(elmToMove, newStartVnode)
                    oldCh[idxInOld] = null
                    api.insertBefore(parentElm, elmToMove.el, oldStartVnode.el)
                }
                newStartVnode = newCh[++newStartIdx]
            }
        }
    }
    if (oldStartIdx > oldEndIdx) { // oldVnode遍历结束了，那就将newVnode里newS指针和newE指针之间的结点添加到oldVnode里
        before = newCh[newEndIdx + 1] == null ? null : newCh[newEndIdx + 1].el
        addVnodes(parentElm, before, newCh, newStartIdx, newEndIdx)
    } else if (newStartIdx > newEndIdx) { // newVnode遍历结束了，那就将oldVnonde里oldS指针和oldE指针之间的结点删除
        removeVnodes(parentElm, oldCh, oldStartIdx, oldEndIdx)
    }
}
```

## Vue 和 React 数据驱动的区别

在数据绑定上来说，vue的特色是双向数据绑定，而在react中是单向数据绑定。

vue中实现数据绑定靠的是数据劫持（Object.defineProperty()）+发布-订阅模式

vue中实现双向绑定

```html
<input v-model="msg" />
```

react中实现双向绑定

```html
<input value={this.state.msg} onChange={() => this.handleInputChange()} />
```

## vue什么阶段能发起请求

- 可以在钩子函数 created、beforeMount、mounted 中进行调用，因为在这三个钩子函数中，data 已经创建，可以将服务端端返回的数据进行赋值。
- 但是推荐在 created 钩子函数中调用异步请求，因为在 created 钩子函数中调用异步请求有以下优点：
  - 能更快获取到服务端数据，减少页面loading 时间；
  - ssr不支持 beforeMount 、mounted 钩子函数，所以放在 created 中有助于一致性；
