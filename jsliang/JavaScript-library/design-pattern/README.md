设计模式
===

> create by **jsliang** on **2018-8-21 11:30:00**   
> Recently revised in **2019-05-31 17:01:56**

## 一 目录

| 章节名  | 导航                                                   |
| ------- | ------------------------------------------------------ |
| 第一章  | [部署开发环境](./design-pattern-chapter01.md)           |
| 第二章  | [面向对象与设计模式初探](./design-pattern-chapter02.md) |
| 第三章  | [工厂模式](./design-pattern-chapter03.md)               |
| 第四章  | [单例模式](./design-pattern-chapter04.md)               |
| 第五章  | [适配器模式](./design-pattern-chapter05.md)             |
| 第六章  | [装饰器模式](./design-pattern-chapter06.md)             |
| 第七章  | [代理模式](./design-pattern-chapter07.md)             |
| 第八章  | [外观模式](./design-pattern-chapter08.md)             |
| 第九章  | [观察者模式](./design-pattern-chapter09.md)             |
| 第十章  | [迭代器模式](./design-pattern-chapter10.md)             |
| 第十一章  | [状态模式](./design-pattern-chapter11.md)             |
| 第十二章  | [其他模式](./design-pattern-chapter12.md)             |
| 第十三章  | [综合应用](./design-pattern-chapter13.md)             |
> 其他模式中包含：原型模式、桥接模式、组合模式、享元模式、策略模式、模板方法模式、职责连模式、命令模式、备忘录模式、中介者模式、访问者模式、解释器模式这 12 种不常用模式。

* 关于面试

面试中能说出第二章至第十一章的模式，一般来说设计模式方面是满分了，当然不排除是高级工程师，但是高级工程师是不会看我这篇文章的，所以 **jsliang** 就不担心被打脸了

* 关于工作日常使用

如果是常用的设计模式，最好就是结合自己的理解，列个列表，在工作中大胆尝试使用，而不是学习完就丢一边。如果是非常用的设计模式，那就应该视业务场景选择性使用。

## 二 使用场景

* 如果是业务性很强的，压根没时间写点好的JavaScript。一般来说，直接用面向对象写法，怎么方便怎么来。所以就有了“活动说明直接整张图丢上去，文字都也不弄出来”“能上图的就上图，写个文字都是罪”
* 然后，如果是长久使用的，要考虑维护的，还是用面向对象思路封装好来，随时调用。

## 三知识普及：  

**Webpack**：

* **babel-core**：把es6中的新语法（箭头函数、rest参数等）解析成ast这种形式，然后配合各个插件分析语法进行相应的处理。
* **babel-loader**：一种loader解析器，配合Webpack解析ES6编写的js文件。
* **babel-preset-\***：babel-reset-2015包含了es6对应的新语法，如果配置了babel-reset-latest，则包含了es2015、es2016、es2017的插件（之后可能包括es2018等）。`注：在安装过程中jsliang发现，官方已不建议使用babel-preset-*系列了，而是推荐使用下面介绍的babel-preset-env包。`
* **babel-polyfill**：实现浏览器对不支持API的兼容（兼容旧环境、填补）。
* **babel-preset-env**：如果不做任何配置，该loader等同于bable-preset-latest，如果你需要根据不同浏览器或者node版本进行配置，推荐使用babel-preset-env进行配置使用 [详情介绍](https://segmentfault.com/a/1190000011639765)

---



