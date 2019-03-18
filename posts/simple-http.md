# 一个简单的 HTTP 工具

## 简介

前端在日常开发中最经常需要遇到的场景便是向后端发送数据、拉取数据，最常用到的 `HTTP Client` 有 `jQuery.ajax`、`axios`、`fetch` 等，不知道大家有没有想过了解它们是基于什么封装的？小二刚毕业的时候也没有想过，当时觉得很多东西 `拿来用` 就对了为什么要知道它们的更多内容？

记得第一次面试时，面试官问了这个问题并给出了提示 `XMLHttpRequest` 但是小二完全答不出来。面试结束后小二很长一段时间不能理解这个问题的意义所在，直到后来用爬取一个站点数据的时候一直出现 “抓取的数据ID 和 直接用数据ID获取的文章内容不一致” 的问题，经过排查后发现是 JavaScript 数字超过一定位数精度丢失：

```javascript
// 输出 { id: 352677239567885440 }
console.log(JSON.parse('{"id":352677239567885445}'))
```

由于是爬取别人的数据肯定没法像自己人一样，直接让后端小哥哥配合改一下传输的数字格式。熟悉 `jQuery.ajax` 和 `axios` 的情况下我们可以`修改配置`、`使用拦截器`、`源码` 来把 json 数据中的数字变为字符串解决这个问题，那如果熟悉 `XMLHttpRequest` 是不是可以自己稍微定制一个？

> 作为一棵树，向下长得越深，向上长得就越高。
> 作为一只程序🐒，知道得更多，BUG 就会更少 XDD。

<!--more-->

`扎深根` 不一定会让我们得到什么，但会让我们遇到问题时更加从容。虽然让我们一起 `扎根 ` 实现一个简单的 `HTTP Client` 来学习 `XMLHttpRequest` 中较为常用的函数方法：

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

## 打赏&联系

如果您感觉有收获，欢迎给我打赏，以激励我输出更多的优质内容。

![打赏&联系](https://raw.githubusercontent.com/pushmetop/resource/master/donate/donate.png)

> 本文原稿来自 [PushMeTop](https://pushmetop.github.io)