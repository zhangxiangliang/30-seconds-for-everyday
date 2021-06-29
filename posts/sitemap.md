<!-- # 投怀送抱 -->

![封面](../images/sitemap/poster.png)

## 简介

> SEO、sitemap、搜索引擎优化、简单教程

在暧昧期和暗恋期时心里总是悬挂着：

* `ta` 为什么还不和我表白？
* `ta` 是不是对我没感觉？
* `ta` 是不是只是把我当备胎？
* `ta` 是不是对谁都这样？

解决问题最简单的方式就是直接 `问问对方`，在 [SEO 初体验](https://juejin.im/post/5ca53dfb6fb9a05e526d8ab7) 中提到过互联网上的网站十六亿多个，如果只靠暗恋的 百度、谷歌的`爬虫小蜘蛛`自己 `主动上门`，显然是很难被第一时间爬取到。

> 与其等待 `主动上门`，不如 `投怀送抱`。 --by 鲁·哪里都有我的·讯

在 `谈恋爱` 中往往会经历一个 互相了解 和 互相磨合 的过程，如果能直接就知道对方家庭情况、兴趣爱好、感情性格等 无疑是非常能够加快了解和磨合，甚至可以提前预知结婚的可能性。

> ps: 小二还是喜欢慢慢了解和磨合。

`sitemap` 便是这么一个 `投怀送抱` 甚至主动告诉小蜘蛛哥哥自己的`银行卡密码`的小可爱，通过 `sitemap` 搜索引擎可以浏览并快速把你所需要被收录的网站爬取下来。

## sitemap

`sitemap` 顾名思义为网站地图，记录网站内的各种链接。只需要把这个文本放到站点的`根目录下`，小蜘蛛哥哥肯定会更容易在人群中发现了解你。接下来介绍 `sitemap` 的多种格式：

### 害羞小妹妹

#### 规则

`txt 文本格式` 害羞小妹妹不敢讲太多的话，她的规则和世界很简单：

* 使用 UTF-8 编码对文件进行编码。
* 文本文件只能包含网址列表。
* 您可以随意对该文本文件进行命名，但前提是要确保它的扩展名为 .txt。

#### 例子

来给你看看她的内心链接：

```txt
http://pushme.top/about
http://pushme.top/i-love-u
http://pushme.top/30-seconds-for-everyday
```

### 知性小姐姐

#### 规则

`xml格式` 知性小姐姐会展示出她的各种感情经历，规则和世界稍微复杂：

| 标签 | | 描述 |
| --- | --- | --- |
| `<urlset>` | 必需 | 包裹 `<url>` 和指明协议 | 
| `<url>` | 必需 | 包裹链接的各种信息，下面出现的标签都是它的子元素 | 
| `<loc>` | 必需 | 页面永久链接地址，必需带上协议(http|https)，长度不超过 2,048 个字符 |
| `<lastmod>` | 可选 | 页面最后修改时间，格式为 `YYYY-MM-DD`，小蜘蛛会根据这个来判断内容是否为最新 |
| `<changefreq>` | 可选 | 页面修改频率，小蜘蛛会稍微参考这个频率来更新内容，可选值 always、hourly、daily、weekly、monthly、yearly、never|
| `<priority>` | 可选 | 链接在站内的权重不会影响在`搜索引擎中的排序`，范围在 0-1 默认值为 0.5，越大表示链接越重要 |

#### 例子

这是她的内心链接，虽然复杂了点但是也容易懂：

```xml
<?xml version="1.0" encoding="UTF-8"?>

<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>http://pushme.top/about</loc>
    <lastmod>2019-01-01</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.8</priority>
  </url>
  
  <url>
    <loc>http://pushme.top/30-seconds-for-everyday</loc>
    <lastmod>2019-01-01</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.8</priority>
  </url>
</urlset> 
```

### 贴心小姐姐

#### 规则

`RSS` 和 `Atom 1.0` 很多博客工具都会带有生成这个的工具，可以使用生成的 `RSS` 来作为站点地图提交，不过要注意 `RSS` 一般只有近期的内容。贴心的小姐姐规则就不阐述了相关工具太多了。

## 使用

这里主要讲解 `百度` 和 `谷歌`，其他搜索引擎小二会找个机会把它们都整理出来。

### 站点

* 根目录下创建 `sitemap.xml` 文件
* 在 `robots.txt` 中添加 `Sitemap: http://domain.com/sitemap.xml`


### 百度

访问百度的`搜索资源平台` 下的 [链接提交](https://ziyuan.baidu.com/linksubmit/index) 界面就可以看到相关的使用方法：

* 手动提交: 规则和 `txt 文本格式`一样。
* 主动推送：调用接口把需要小蜘蛛爬取的网站直接发送给百度。
* 自动推送：在页面上加载百度的 `https://zz.bdstatic.com/linksubmit/push.js` 脚本，当页面被访问时脚本会自己发送当前链接到搜索引擎。
* sitemap: 提交自己站点的 sitemap 相关文件。

### 谷歌

* 使用Search Console [站点地图工具](https://search.google.com/search-console/not-verified) 将其提交给 Google
* 使用“ping”功能要求我们抓取站点地图。发送如下所示的 HTTP GET 请求：`http://www.google.com/ping?sitemap=<complete_url_of_sitemap>`，例如：`http://www.google.com/ping?sitemap=https://example.com/sitemap.xml`。

## SEO 相关内容

* [H1 の 小秘密](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/heading.md)
* [SEO 初体验](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/seo-101.md)
* [img の 小九九](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/img-tag.md)
* [千里姻缘一线牵](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/hyperlink.md)
* [投怀送抱](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/sitemap.md)
* [漫游器法则](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/robot-txt.md)

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/zhangxiangliang/30-seconds-for-everyday) 给个 `小星星`。

> 本文原稿来自 [ZhangXiangLiang](https://github.com/zhangxiangliang)
