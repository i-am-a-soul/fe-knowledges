Markdown 打造静态网站
===

> Create by **jsliang** on **2019-5-29 08:08:12**  
> Recently revised in **2019-05-30 19:15:45**

## 一 序

Markdown 是一种可以使用普通文本编辑器编写的标记语言，通过简单的标记语法，它可以使普通文本内容具有一定的格式。

这么一说小伙伴们可能有点懵逼，还没搞懂 Markdown 是啥。

那么，换种说法：

**Markdown 是一个简写版的 HTML，它内置了一套自己的规则，不需要你编写复杂的 CSS 也能很好地渲染阅读，你还可以在其内嵌其他的 HTML 标签、CSS 样式和 JS 脚本。**

这么说小伙伴们会不会对它有比较清晰的印象了。

正基于此，我们用 Markdown 写笔记的同时，还可以将 Markdown 转换成 `*.html` 文件，然后部署在 GitHub Pages 等一些免费的静态服务器上，从而形成静态网站。

> 当然，不仅仅可以写 HTML，还可以写 JS，还可以使用 Ajax 调用后端接口，搞搞留言等功能，就是一个完整的博客、论坛……

如果小伙伴们感觉还是有点小小的困惑，那么咱列几个例子：

* [腾讯 Web 前端团队](http://alloyteam.github.io/)
* [GitHub Games](http://likexia.gitee.io/game/)

当然，还有 **jsliang** 将自己写的 Markdown 文档库，通过 Gitbook 转换成的静态网站：

* [jsliang 的文档库小册](https://liangjunrong.github.io/)

看到这里，小伙伴内心是不是跃跃欲试了~

## 二 涉及知识点

本系列教程涉及知识点：

* Markdown
* GitHub Pages
* Git
* npm
* VuePress
* GitBook

## 三 目录

**不折腾的前端，和咸鱼有什么区别！**

| 目录 | 简介 |
| --- | --- |
| [Markdown](./Markdown/README.md) | 扎实的 Markdown 基础可以让你更快速地编写笔记。 |
| [GitHub Pages](./GitHub-Pages/README.md) | 本系列文章最终目标，将内容部署到 GitHub Pages 上。 |
| [VuePress](./VuePress/README.md) | 享受 Vue + Webpack + Markdown 的开发体验。 |
| [GitBook](./GitBook/README.md) | 你只需要专注于编写文档，其他交给我们！ |

看完这四个部分，你应该对于怎么打造一个静态博客/文档库的步骤了然于胸了，**jsliang** 觉得你可以行动起来啦！

当然，将 Markdown 转成 HTML 文件的不仅仅限于 VuePress 和 GitBook，或许你还可以自行探索 Hexo 等静态网站生成器，在这里 **jsliang** 表示自己的精力不足，就不给小伙伴们当先驱啦~

---



