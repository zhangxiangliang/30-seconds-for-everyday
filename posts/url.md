<!-- # URL大爆炸 -->

![封面](../images/url/poster.png)

## 简介

> URL结构、组成、query、hash、axios数组传递错误、HTTP 请求

伴随着微信消息的提示音 `小四` 发来一段代码说 `不知道为什么请求不到页面数据`：

```javascript
axios.get('users', {
    params: { ids: [1, 2, 3] }
})
```

小二一看大概率是 `query` 中`数组`传递方式引起的，由于后端实现解析数组 `ids:[5, 6, 100]` 可能有以下几种方式：

* bracket: `ids[]=1&ids[]=2&ids[]=3`
* index: `ids[0]=1&ids[1]=2&ids[3]=3`
* comma: `ids=1,2,3`
* none: `ids=1&ids=2&ids=3`

小四分别测试后便把问题解决了，这也让小二想起 `小熊猫哥哥` 在开发的时候，也遇到过这个问题网上一搜发现别人用 [qs](https://www.npmjs.com/package/qs) 库中的 `stringify` 直接代码一试`没报错能运行`，不管它的原理是什么，现在想想挺可怕的。

> 虽然天天和 `URL` 打交道但并不是所有人都懂它。

> 对于为什么代码能运行也不是所有人都会去`深究它`。

## 现原形

利用 `URL()` 对象可以快速的把一个 `url地址` 打回原形：

##### 脚本

```javascript
const url = new URL('http://www.pushme.top/users?sort_by=asc#page=userlist')
console.log(url)
```

##### 输出

```javascript
{
    hash: "#page=userlist"
    host: "www.pushme.top"
    hostname: "www.pushme.top"
    href: "http://www.pushme.top/users?sort_by=asc#page=userlist"
    origin: "http://www.pushme.top"
    password: ""
    pathname: "/users"
    port: ""
    protocol: "http:"
    search: "?sort_by=asc"
    searchParams: URLSearchParams {}
    username: ""
}
```

没想到吧 小小的一段 `url地址` 里面居然有这么多属性，在这里主要会讲解的 `hash` 和 `search`。

> 推荐打开控制台把脚本运行一下，这样阅读的时候就不需要上下对照查看了。

## host 和 hostname

眼尖的同学肯定发现了 `host` 和 `hostname` 居然一模一样这是为什么呢？

回忆一下开发经常在见到的 `localhost:8080`，这里出现了端口号 `8080` 而平时使用访问一些网站的时候却没有带上端口号。这是因为 `url地址` 会默认端口号为 `80`，所以你仔细看看会发现上面 `port` 的值为空。

而 `host` 和 `hostname` 的区别便是有 `port` 的时候 `host` 会包含端口号，而 `hostname` 不会包含。

## protocol 和 origin

`protocol` 指的便是 `协议` 最常见的有 `http` 和 `https`，当然现在浏览器再不输入协议时会自动帮你加上，不过在 `URL()` 不带上协议可是会报错的哦。`origin` 则为 `protocol` 和 `host` 拼接组成。

## search 和 searchParams

#### 基础

`?search=a` 中 `query` 以第一个`?`开始至`行尾`或`#`结束。用于向后端传递一些数据，数据使用 `&` 进行分隔，值使用 `=` 分隔。通过一段代码来理解一下：

```javascript
const query = 'id=1&sort=asc&hello=world';
// 对 & 分割取得数据对
const data = query.split('&').reduce((data,keyValue) => {
    const [ key, value ] = keyValue.split('=');
    return (data[key] = value, data);
}, {});

// 输出 {id: "1", sort: "asc", hello: "world"}
console.log(data);
```

这就是 `query` 最基础的数据对的组合方式，当然开头的四种 `数组` 的表达方式需要进行另外的处理，无外乎就是对 `key` 的收集 和 `value` 的判断。不过这部分基本上后端的框架都帮我们处理好了，前端也可以使用 `qs`、`query-string`、`qss` 等库来完成。

> 题外话：这几个库代码都挺少的，值得一读说不定有新收获。

#### 加号与空格

每天使用的 `百度` 和 `谷歌` 中不知道大家有没有主要到这几个细节：

* 输入 `https://www.baidu.com/s?wd=小二+pushmetop` 搜索框中出现的是`小二 pushmetop`，地址栏中url地址的 `+` 神奇的变成了 `空格`。
* 输入 `https://www.baidu.com/s?wd=小二 pushmetop` 搜索框中出现的是`小二 pushmetop`，地址栏中url地址的 `空格` 的变成 `%20`。
* 输入 `https://www.baidu.com/s?wd=小二%2Bpushmetop` 搜索框中出现的是`小二+pushmetop`，地址栏中url地址的 `%2B` 的变成 `+`。

具体原因可以查看 [维基百科](https://zh.wikipedia.org/wiki/%E7%99%BE%E5%88%86%E5%8F%B7%E7%BC%96%E7%A0%81) 关于 `保留字符的百分号编码` 。

#### URL 编码

在 `掘金` 等网站点击链接都会快速的闪现类似 `http://www.pushmetop.com?redirect=xxxxx` 的 `url地址`，会发现 `redirect` 对应的重定向地址会是一堆夹带 `%` 的乱码这是为什么呢？

让我们假设需要跳转的链接是 `www.test.com?hello=world&id=1`,把整个链接拼接起来则为：

```
http://www.pushmetop.com?redirect=www.test.com?hello=world&id=1
```

根据一开始的定义 `解析值` 和 `预期值` 完全不同了：

##### 解析值
```json
{
    "redirect": "www.test.com?hello=world",
    "id": "1"
}
```

##### 预期值
```json
{
    "redirect": "www.test.com?hello=world&id=1"
}
```

为了解决这个问题便诞生了 `URL编码` 来解决问题：

*  `encodeURIComponent()` 和 `decodeURIComponent()` 推荐使用。
*  `encodeURI()` 和 `decodeURI()` 对比前者不会对 `"; / ? : @ & = + $ , #"` 这些字符编码。
*  `escape()` 和 `unescape()` 不推荐使用。

##### 例子

```javascript
let redirect = 'www.test.com?hello=world&id=1';
redirect = encodeURIComponent(redirect);

let url = `http://www.pushmetop.com?redirect=${redirect}`;
url = new URL(url)

// 输出: www.test.com?hello=world&id=1
console.log(url.searchParams.get('redirect'))
```

## hash

`#hash` 中 `fragment` 以 `#` 为开始 `行尾` 为结束。在 [回到顶部](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/scroll.md) 中有提到过利用hash锚点来进行跳转，如果大家注意观察的话会发现 `hash` 的改变不会引起页面的刷新。

在 `Angular.js`、`Vue Router` 等库中，会利用在 `html5` 中提供了 `history` 的一系列操作，来帮助我们不刷新页面管理  `url`。但是在一些旧的浏览器上并不兼容时，会利用 `hash` 不会主动触发浏览器 `reload` 的特性来修改 `location.hash` 来管理路由。 当然 `hash` 的另外一个特点是可以被保存为书签。

`hash` 的小妙用也可以像 `query` 那样利用 `&` 和 `=` 来存取数据，当然你也可以定制属于你的规则。

## href 和 pathname

`href` 为整个 `url地址`。而 `pathname` 属性包含 URL 的整个路径部分。它跟在 `host` （包括 `port`）后面，排在 `query` 或 `hash` 组成部分的前面且被 ASCII 问号（?）或哈希字符（#）分隔。

## username 和 password

`username` 和 `password` 在日常使用中很少用，它们可以合称为 `auth`。该字符串跟在 `protocol` 和双斜杠（如果有）的后面，排在 `host` 部分的前面且被一个 ASCII 的 at 符号（@）分隔：

```
http://username:password@www.pushme.top/test/blah?something=123
```

## 结尾

本来只是想讨论 `hash` 和 `search` ，结果全都过一遍，今天就辛苦大家了。

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/zhangxiangliang/30-seconds-for-everyday) 给个 `小星星`。

> 本文原稿来自 [ZhangXiangLiang](https://github.com/zhangxiangliang)
