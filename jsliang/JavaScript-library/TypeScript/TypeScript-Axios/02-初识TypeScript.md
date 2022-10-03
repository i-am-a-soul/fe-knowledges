02 - 初识 TypeScript
===

> Create by **jsliang** on **2020-3-3 07:49:30**  
> Recently revised in **2020-03-05 16:38:20**

## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| [二 前言](#chapter-two) |
| [三 TypeScript 的特点](#chapter-three) |
| [四 安装 TypeScript](#chapter-four) |
| [五 快速入门](#chapter-five) |
| &emsp;[5.1 编译代码](#chapter-five-one) |
| &emsp;[5.2 报错提示](#chapter-five-two) |
| &emsp;[5.3 类型注解](#chapter-five-three) |
| &emsp;[5.4 接口](#chapter-five-four) |
| &emsp;[5.5 类](#chapter-five-five) |
| [六 总结](#chapter-six) |

## 二 前言



TypeScript 作为 JavaScript 语言的超集，它为 JavaScript 添加了可选择的类型标注，大大增强了代码的可读性和可维护性。

同时，它提供最新和不断发展的 JavaScript 特性，能让我们建立更健壮的组件。

## 三 TypeScript 的特点



TypeScript 主要有 3 大特点：

* 始于 JavaScript，归于 JavaScript

TypeScript 可以编译出纯净、简洁的 JavaScript 代码，并且可以运行在任何浏览器上、Node.js 环境中以及任何支持 ECMAScript 3（或者更高版本）的 JavaScript 引擎中。

* 强大的工具构建大型应用

类型允许 JavaScript 开发者在开发 JavaScript 应用程序时使用高效的开发工具和常用操作。比如静态检查和代码重构。

类型是可选的，类型推断让一些类型的注释使你的代码的静态验证有很大的不同。

类型让你定义软件组件之间的接口和洞察现有 JavaScript 库的行为。

* 先进的 JavaScript

TypeScript 提供最新的不断发展的 JavaScript 特性，包括那些来自 2015 年的 ECMAScript（ES6）和未来的提案中的特性，比如异步功能和 Decorators，以帮助建立健壮的组件。

这些特性在高可信应用程序开发时事可用的，但是会被编译成简洁的 ECMAScript3（或更高版本）的 JavaScript。

总结：TypeScript 在社区的流行度度越来越高，它非常适用于一些大型项目，也非常适用于一些基础库，极大地帮助我们提升了开发效率和体验。

## 四 安装 TypeScript



1. 安装 Node.js
2. 安装 TypeScript：`npm i typescript -g`
3. 查看版本：`tsc -V`（Version 3.8.3）

## 五 快速入门



在这部分，我们会通过下面 4 点来进行快速了解：

* 编译代码
* 报错提示
* 类型注解
* 接口
* 类

### 5.1 编译代码



新建文件夹 `ts-axios`，在里面建立一个 `index.ts`：

> ts-axios/index.ts

```ts
function sayHello(person) {
  return 'Hello ' + person;
}

const user = 'jsliang';

console.log(sayHello(user));
```

然后对该文件进行编译：

```shell
tsc index.ts
```

这时候文件夹 `ts-axios` 下会添加一个文件：

* `ts-axios/index.js`

打开看到：

```js
function sayHello(person) {
    return 'Hello ' + person;
}
var user = 'jsliang';
console.log(sayHello(user));

```

看不出有啥变化？那试试 ES6 语法：

> ts-axios/index.ts

```ts
const getName = (s, n) => {
	return s.split(' ').findIndex(item => item === n);
}

const str = 'I\' m jsliang';
const user = 'jsliang';

console.log(getName(str, user));
```

通过 `tsc index.ts` 编译文件后，生成 `index.js` 文件如下：

> ts-axios/index.js

```js
var getName = function (s, n) {
    return s.split(' ').findIndex(function (item) { return item === n; });
};
var str = 'I\' m jsliang';
var user = 'jsliang';
console.log(getName(str, user));

```

可以看出 ES6 的箭头函数语法变成了 ES5 的函数方法，当然，不止如此，下面我们会逐步探索了解。

### 5.2 报错提示



在进一步了解 TypeScript 特性之前，我们有必要了解下 TypeScript 的报错机制：

> ts-axios/index.ts

```ts
function sayHello(person: string) {
  return 'Hello ' + person;
}

console.log(sayHello([1, 2, 3]));
```

通过 `tsc index.ts` 编译后发现控制台提示：

```shell
index.ts:5:22 - error TS2345: Argument of type 'number[]' is not assignable to parameter of type 'string'.

5 console.log(sayHello([1, 2, 3]));
                       ~~~~~~~~~

Found 1 error.
```

可以看出我们期望的是 `string` 字符串类型，但是我们传递了 `number[]` 数字数组类型，所以 TypeScript 给我们进行了报错提醒。

当然，虽然编译报错了，但是 TypeScript 会如实打包。

> ts-axios/index.jw

```js
function sayHello(person) {
    return 'Hello ' + person;
}
console.log(sayHello([1, 2, 3]));

```

当然，我们还是希望自己能重视控制台的报错提示，去修复它，从而减少我们开发过程中出现的问题。

### 5.3 类型注解



在上面报错提示的学习中，我们看到了一句话：

```ts
function sayHello(person: string) {
  return 'Hello ' + person;
}
```

那么这个：`person: string`，相信小伙伴们在看上面代码的时候已经了解了，它就是类型注解。

TypeScript 中的类型注解是一种轻量级的为函数或者变量添加约束的方式。

在 `person: string` 中的意思就是，我们希望 `person` 传入的类型值为字符串，而不是 `[1, 2, 3]` 这种 `number[]` 或者其他内容。

### 5.4 接口



接下来我们进行接口的定义，先看代码：

> ts-axios/index.ts

```ts
interface Person {
  firstName: string;
  lastName: string;
}

function sayHi(person: Person) {
  return 'Hello ' + person.firstName + person.lastName;
}

let user = {
  firstName: 'Liang',
  lastName: 'Junrong',
};

console.log(sayHi(user));

// 1. cmd：tsc index.ts
// 2. cmd：node index.js
// 3. console：Hello LiangJunrong
```

此时执行 2 个 `shell` 命令：

```shell
tsc index.ts

node index.js
```

打印：

```
Hello LiangJunrong
```

看到这里，我们应该略有感想：

* 类型注解和接口，就是一个 `function()` 定义的时候进行设置，一个将这些限制提取出来，放到 `interface` 中。

> 两者区分

```ts
function sayHi(name: string, age: number) {
  return `人物：${name} ${age} 岁`;
}
console.log(sayHi('梁峻荣', 25));

interface User {
  name: string;
  age: number;
}
function sayHello(user: User) {
  return `人物：${user.name} ${user.age} 岁`;
}
console.log(sayHello({ name: 'jsliang', age: 25 }));
```

### 5.5 类



最后，我们了解下 TypeScript 中一个重要的点：类。

类不难理解，所谓物以类聚人以群分，而我们的类就是区分不同的功能实现。

下面举例 `User` 类：

> ts-axios/index.ts

```ts
class User {
  firstName: string;
  lastName: string;

  constructor (firstName: string, lastName: string) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}

const user = new User('Liang', 'Junrong');

console.log(user.firstName); // Liang
console.log(user.lastName); // Junrong
```

通过 `shell` 命令编译后：

```shell
tsc index.ts
node index.js
```

查看 `index.js`：

> ts-axios/index.ts

```js
var User = /** @class */ (function () {
    function User(firstName, lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }
    return User;
}());
var user = new User('Liang', 'Junrong');
console.log(user.firstName);
console.log(user.lastName);

```

查看 `Console`：

```
Liang
Junrong
```

可以看出 `Class` 本质上还是 JavaScript 函数的实现，它只是 TypeScript 中的一个语法糖。

## 六 总结



到此，我们就快速了解了 TypeScript 的一些基础内容。

* TypeScript 安装
* TypeScript 的特点
* TypeScript 快速入门

那么，我们下面将会进一步探索。


