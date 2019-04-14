<!-- # 简单的 HTTP 工具 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/simple-http/poster.png)

## 简介

> XMLHttpRequest、HTTP 工具原理、XHR

`jQuery.ajax`、`axios` 和 新的 Web API `fetch` 在浏览器不支持的兼容代码都是利用 
 `XMLHttpRequest` 来完成网络请求，今天一起来实现一个简单的 `HTTP 请求客户端` 顺便学习`XMLHttpRequest` 中较为常用的函数方法：

```javascript
const http = ({
  url,
  callback,
  data=null,
  method='GET',
  err = console.error,
}) => {
    const request = new XMLHttpRequest();
    request.open(method, url, true);
    request.setRequestHeader('Content-type', 'application/json; charset=utf-8');
    request.onerror = () => err(request);
    request.onload = () => callback(request.responseText);
    request.send(data ? JSON.stringify(data) : null);
};
```

## 代码分析

函数为接受一个对象参数，而不是像 `(url, callback)` 这样的参数列表？因为使用对象相对参数列表来说不用`刻意`的去记参数的顺序只需要记住所需数据：

> 小技巧：根据情况利用对象参数来代替参数列表。

```javascript
const http = ({
  url,
  callback,
  data=null,
  method='GET',
  err = console.error,
}) => {
    // ...
};
```

创建 `XMLHttpRequest` 对象并使用 `XMLHttpRequest.open()` 方法初始化一个请求（这里的 method 可以是 GET、POST、PUT、DELETE）：

```javascript
const request = new XMLHttpRequest();
request.open(method, url, true);
```

设置 Request Header 中的内容类型：

```javascript
request.setRequestHeader('Content-type', 'application/json; charset=utf-8');
```

当请求完成时利用 `回调函数` 来执行外部传入的代码：

> 小技巧：善用用回调函数。

```javascript
request.onerror = () => err(request);
request.onload = () => callback(request.responseText);
```

发送需要带上的数据：

```javascript
request.send(data ? JSON.stringify(data) : null);
```

#### 使用场景

手痒的同学可以开始动手加上 `Promise` 或者按照 `axios API` 实现一个自己的 `HTTP Client`，好奇宝宝可以试试阅读相关 `axios`、`fetch` 源码。下面给出几个使用例子：

```javascript
http({
    method: 'POST',
    url: 'http://pushme.top/api/v1/posts',
    callback: console.log, 
    data: { title: 'hello', content: 'hello world'}
})

http({
    method: 'GET',
    url: 'http://pushme.top/api/v1/posts',
    callback: console.log, 
})
```

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。
* 如果您想与小二更多交流添加微信 `m353839115`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)