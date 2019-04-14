<!-- # 漫游器法则 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/robot-txt/poster.png)

## 简介

> SEO、robot.txt、搜索引擎优化

在浩海的互联网世界中：

* 互联网 宛如 宇宙
* 站点 宛如 星系
* 网页 宛如 星球
* 网页内容 宛如 生灵万物

而在互联网世界漫游的`搜索引擎`爬虫小蜘蛛，就好比一搜穿梭在宇宙里的星际`漫游器`，想想是不是还挺浪漫的。对于不同的星系有着自己的规则，如果不准守规则，小心自动防御功能把 `漫游器` 打坏哦~

> 小二幻想过这个世界如果是由代码组成的，还是挺有意思的，很多灵异事件都可以解释为 `bug`，有次和同学脑洞大开聊了一晚上，有机会可以找个时间来构筑一个代码 `世界观`。

## 漫游器法则

每个星系的入口处即`网站根目录`都会设置一个 `robot.txt` 又叫做`漫游器法则`，记录漫游器应该准守的规则。`漫游器法则` 更多的是一个协定，并不是写了所有的爬虫都会准守这个规则。

很多公司或者个人在没有内容输出时，往往会通过 `爬虫` 去爬取别人站点的数据，如果准守规则也可以叫其 `漫游器`，但是不准守规则肆无忌惮爬取的称之为 `海盗船`。被爬取的站点，对于这些 `海盗船` 会做出一定的判断，或者`访问评率`限制来保护自己。

### 名单法则

在 `robot.txt` 中通过 `User-agent` 来规定那些 `漫游器` 应该准守哪些规则，使用 `*` 星号表示允许所有 `漫游器` 都应该准守例如`User-agent: *`。也可以对特定的漫游器做出限制，例如对 `百度漫游器` 做出限制 `User-agent: Baiduspider`。在名单法则之下是与之对应的 `允许法则` 和 `拒接法则`：

* 允许法则通过 `Allow:` 配合路径法则来告诉 `漫游器` 哪些链接是`应该`爬取访问的。
* 拒接法则通过 `Disallow:` 配合路径法则来告诉 `漫游器` 哪些链接是`不应该`爬取访问的。

### 路径法则

对 `pathname` 组成 `query` 的路径，配合上 `*` 和 `$` 符号可以拼凑出一条网站路径规则。下面给出几个例子：

* 用户列表 `https://pushme.top/users` 用路径表达 `/users`
* 文章评论 `https://pushme.top/posts/1/comments` 用路径表达 `/posts/*/comments`
* 样式文件 `https://pushme.top/assets/styles/main.css` 用路径表达 `/assets/styles/*.css$`
 
> 更多 URL 详细内容可以查看 [URL 大爆炸](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/url.md)

### 星系推荐法则

在 [投怀送抱](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/sitemap.md) 中介绍了 `sitemap` 网页地图，用于告诉`漫游器`哪些网站哪些页面值得访问。通过 `Sitemap:` 来指定 `Sitemap: https://pushme.top/sitemap.xml`。

### 单双号法则

网站和现实生活一样也有分 `单双号`，`漫游器` 和 `海盗船` 爬取页面也会占用到服务器的资源。如果占用太多资源会导致 `正常用户` 无法访问网站，所以利用 `单双号法则` 来限制 `漫游器` 的访问频率：

* `Crawl-delay: n` 每次抓取间隔n秒。
* `Request-rate: x/n` 抓取x个页面在n秒之内。

## 掘金漫游器法则

在讲完了整体的`漫游器法则`构成，让我们一起阅读一下 `掘金漫游器法则`。访问 `https://juejin.im/robots.txt` 就可以看到如下内容：

```
User-agent: *
Request-rate: 1/1
Crawl-delay: 5

Disallow: /timeline
Disallow: /submit-entry
Disallow: /new-entry
Disallow: /edit-entry
Disallow: /notification
Disallow: /subscribe/subscribed
Disallow: /user/settings
Disallow: /reset-password
Disallow: /drafts
Disallow: /editor
Disallow: /user/invitation
Disallow: /user/wallet
Disallow: /entry/*/view$
Disallow: /auth
Disallow: /oauth
Disallow: /zhuanlan/*?sort=newest
Disallow: /zhuanlan/*?sort=comment
Disallow: /search
Disallow: /equation
```

可以看到`掘金漫游器法则`还是相对宽松的，限制了访问评率和不应该访问网页，没有对具体的 `百度漫游器` 和 `谷歌漫游器` 等作出限制，所以同学也可以写 `漫游器` 来爬取掘金的部分内容。比如今天的沸点中就看到了：

![今日掘学](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/robot-txt/juejin.png)

## SEO 相关内容

* [H1 の 小秘密](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/heading.md)
* [SEO 初体验](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/seo-101.md)
* [img の 小九九](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/img-tag.md)
* [千里姻缘一线牵](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/hyperlink.md)
* [投怀送抱](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/sitemap.md)
* [漫游器法则](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/robot-txt.md)

## 其他

关于 `robot.txt` 生成的工具这里推荐 [robots文件生成](http://tool.chinaz.com/robots) 简单易用。

小二在这里只讨论了一些 `力所能及` 且 `容易做到` 的 SEO 内容，关于 SEO 相关的内容就讨论到这里了。虽然 `语义化标签` 这部分内容也对 SEO 有所帮助，但是实践起来挺难做到的，如果小二有想简单且容易理解的方法到时候再补上这篇。

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。
* 如果您想与小二更多交流添加微信 `m353839115`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)