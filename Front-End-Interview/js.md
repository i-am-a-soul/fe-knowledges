[toc]

## 事件对象中的clientX offsetX screenX pageX的区别

- [clientX, clientY]

```txt
client直译就是客户端，客户端的窗口就是指游览器的显示页面内容的窗口大小（不包含工具栏、导航栏等等）
[clientX, clientY]就是鼠标距游览器显示窗口的长度

兼容性：IE和主流游览器都支持。
```

- [offsetX, offsetY]

```txt
offset意为偏移量
[offsetX, offsetY]是被点击的元素距左上角为参考原点的长度，而IE、FF和Chrome的参考点有所差异。

Chrome下，offsetX offsetY是包含边框的
IE、FF是不包含边框的，如果鼠标进入到border区域，为返回负值

兼容性：IE9+,chrome,FF都支持此属性。
```

- [screenX, screenY]

```txt
screen顾名思义是屏幕
[screenX, screenY]是用来获取鼠标点击位置到屏幕显示器的距离，距离的最大值需根据屏幕分辨率的尺寸来计算。

兼容性：所有浏览器都支持此属性。
```

- [pageX, pageY]

```txt
page为页面的意思，页面的高度一般情况client浏览器显示区域装不下，所以会出现垂直滚动条。

[pageX, pageY]是鼠标距离页面初始page原点的长度。

在IE中没有pageX、pageY取而代之的是event.x、event.y。x和y在webkit内核下也实现了，所以火狐不支持x，y。

兼容性：IE不支持，其他高级浏览器支持。
```

## js判断图片是否加载完毕的方式

- load事件

> 测试，所有浏览器都显示出了“loaded”，说明所有浏览器都支持img的load事件。

```html
<img id="img" src="https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=151472226,3497652000&fm=26&gp=0.jpg">
<p id="p">loading...</p>
<script>
    document.getElementById('img').onload = function() {
        document.getElementById('p').innerHTML = 'loaded';
    }
</script>
```

- readystatechange事件

> readyState为complete和loaded则表明图片已经加载完毕。测试IE6-IE10支持该事件，其它浏览器不支持。

```html
<img id="img" src="https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=151472226,3497652000&fm=26&gp=0.jpg">
<p id="p">loading...</p>
<script>
    var img = document.getElementById('img');
    img.onreadystatechange = function () {
        if (img.readyState == 'complete' || img.readyState == 'loaded') {
            document.getElementById('p').innerHTML = 'readystatechange:loaded';
        }
    }
</script>
```

- img 的 complete属性

> 轮询不断监测img的complete属性，如果为true则表明图片已经加载完毕，停止轮询。该属性所有浏览器都支持。

```html
<img id="img" src="https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=151472226,3497652000&fm=26&gp=0.jpg">
<p id="p">loading...</p>
<script>

    function imgLoad(img, callback) {
        var timer = setInterval(function() {
            if (img.complete) {
                callback(img);
                clearInterval(timer);
            }
        }, 50)
    }
    imgLoad(img, function() {
        document.getElementById('p').innerHTML = '加载完毕';
    })
</script>
```

## js 延迟加载的方式有哪些

> js 延迟加载，也就是等页面加载完成之后再加载 JavaScript 文件。 js 延迟加载有助于提高页面加载速度。

一般有以下几种方式：

- defer 属性
- async 属性
- 动态创建 DOM 方式
- 使用 setTimeout 延迟方法
- 让 JS 最后加载

## Ajax 禁用浏览器的缓存功能

> 项目中，一般提交请求都会通过 ajax 来提交，我们都知道 ajax 能提高页面载入的速度主要的原因是通过 ajax 减少了重复数据的载入，也就是说在载入数据的同时将数据缓存到内存中，一旦数据被加载其中，只要我们没有刷新页面，这些数据就会一直被缓存在内存中，当我们提交 的 URL 与历史的 URL 一致时，就不需要提交给服务器，也就是不需要从服务器上面去获取数据，虽然这样降低了服务器的负载提高了用户的体验，但是我们不能获取最新的数据。为了保证我们读取的信息都是最新的，我们就需要禁止他的缓存功能。

解决的方法有：

1. 在 ajax 发送请求前加上 `xhr.setRequestHeader("If-Modified-Since","0")`。
2. 在 ajax 发送请求前加上 `xhr.setRequestHeader("Cache-Control","no-cache")`。
3. 在 URL 后面加上一个随机数： `"fresh=" + Math.random()`;。
4. 在 URL 后面加上时间戳：`"nowtime=" + new Date().getTime()`;。
5. 如果是使用 jQuery，直接这样就可以了`$.ajaxSetup({cache:false})`。这样页面的所有 ajax 都会执行这条语句就是不需要保存缓存记录。

