<!-- # 千里姻缘一线牵 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/hyperlink/poster.png)

## 简介

> SEO、链接、a 标签、HTTP 状态码、link 标签、alternate、canonical

`唐朝`有个小伙叫韦固喜欢在河边玩，一天遇到一个老伯伯在月光下把两块石头系在一起。小伙看到很好奇便问道“系石头做什么呢？”老伯伯说“我在给当婚人牵线，这对石头是一对夫妻。”小伙问道：“那我的妻子是谁呢？”老伯伯说：“就是村头看菜园子的女孩儿。”

小伙就好气，本小伙`玉树临风、风流倜傥`怎么可以和菜园穷丑丫头一起呢？第二天路过菜园，抄起石头就往女孩儿头上砸过去，女孩儿便倒地不起，小伙也吓得畏罪潜逃。

后来小伙当了大学士，看上了张员外的外甥女拖媒人提请。洞房花烛夜时发现`妻子头上有个疤痕`，问道怎么回事。才发现原来这就是菜园的穷丑丫头，把月下老伯的话告诉了妻子，才相信缘分是拆不散的。

这个便是 `千里姻缘一线牵` 故事来源，这要是换到现在怕是 `想去医院看看 wifi 快不快了`。不过这句话常说，但是故事并不是所有人都知道，大家可以讲给女朋友听听加点小内容，肯定撩妹满分。

> 程序员心中的女神是计算机，怎么会有女朋友呢？-- by 又背锅的鲁迅先生

## 链接网

### 是什么

本来只想讲 `a 标签`，但是其他内容关联性也挺强的，所以本文篇幅会比较大。

为什么会取这个标题呢？在使用网络的时候，一个个网站通过 `链接` 被连接到一起，好似月老的红线一圈圈的缠绕着。有时候不得不佩服中文的博大精深，`互联网` 这个词真的是非常恰当 通过 `链接` 互相联系 在一起的网状结构。

> 怀旧的同学可以看看《天庭外传》小猪八戒牵红线那段真的是笑死小二了。

### 为什么

当 `搜索引擎` 派出 `小蜘蛛` 在爬取`当前链接`页面时，页面上会有很多其他`相关链接`，`小蜘蛛` 会顺着这个链接继续爬取下去到一定的深度，并对这些`相关链接`和 `当前链接`做出关联，相关链接的好坏会影响到`当前链接`的自然排名。

举个最简单的例子，闽南风俗里在结婚前有个 `考察环节`，男女方各自会组成`相亲考察团`到对方的村里面打听 `对方` 人品、行为等在邻居口中的评价来从`侧面`了解对方的情况。

小二的朋友小四因为外婆在几十年前 `偷过一只鸭` 被邻居告知了 `考察团`，导致 `相亲考察团` 对他的印象分有所降低。这里的 `外婆` 和 `小四` 便是 `相关链接` 和 `当前链接` 的映照。

### a 标签

在页面上出现的链接几乎离不开 `a 标签`，我们通过一个个的 `a 标签` 去往不同的页面。大家最经常使用也是最经常忽略的便是 `a 标签` 中的文本内容，当 `搜索引擎` 中的 `小蜘蛛` 爬取当前页面，发现页面上有 `a 标签` 时会继续爬取下去，而文本内容会作为链接的描述参考。

一般的链接结构是`<a href="https://juejin.im/timeline/frontend" >前端</a>`。其中`前端`就是文本内容也叫做`锚文本`，通常情况下`搜索引擎`会通过`锚文本`来理解`https://juejin.im/timeline/frontend`这个页面的内容是什么。为了告诉 `小蜘蛛` 哪些可以爬取哪些不可以爬取，可以利用 `rel` 来指明：

| rel 值 | 解释 |
| --- | --- |
| external | 表示这是一个站外链接 |
| nofollow | 搜索引擎 `不应该` 抓取 `相关链接` 并记录权重。|
| noopener、noreferrer | 使得 opener 和 referrer 属性无效，防止 target="_ blank" 带来钓鱼安全问题 |

例如在掘金中用户评论中使用 `noopener、noreferrer` 和 `nofollow` 来防止评论链接里使用了一些危险链接：


![用户评论](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/hyperlink/comments.png)

> `target="_ blank"` 相关内容可以查看 [大家一起被捕吧](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/lets-get-arrested.md)。


### 友链

`相关链接` 除了坏处也有好处，如果是一个`知根知底`且`不错`的网站，可以相互关联来提升网站的权重，这个方式叫做`友情链接` 从名字上就非常好理解。像`京东` 就有专门的友情链接 `http://club.jd.com/links.aspx`：

![京东](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/hyperlink/jd.png)

友情链接的好处简单说来就是：一个网站被越多站点提及，越知名站点提及，它很大程度上是一个好网站。例如 `BAT` 要是挂上了小二的链接，大家是不是也会更相信小二这个人？

### robots

利用 `robots.txt` 来告诉 `小蜘蛛` 哪些页面是可以爬取的那些是不可以爬取的:

```
User-agent: *

# agency和user禁止访问
Disallow: /timeline
Disallow: /submit-entry
Disallow: /new-entry
Disallow: /edit-entry
Disallow: /notification
Disallow: /subscribe/subscribed

# agency中允许访问的目录
Allow: /agency/join
Allow: /agency/personal
```

### meta robots

如果想`当前链接` 和 `相关链接` 完全不出现在搜索结果中，例如可以利用 `meta` 标签：

```html
<meta name="robots" content="onindex,nofollow">
```

name 和 content 值部分参考如下：

#### name 值

| name 值 | 解释 |
| --- | --- |
| robots | 泛指所有小蜘蛛 |
| Baiduspide | 指百度小蜘蛛 |
| Googlebot | 指谷歌小蜘蛛 |

#### content 值

| content 值 | 解释 |
| --- | --- |
| index | 搜索引擎 `应该` 抓取该 `当前链接` |
| noindex | 搜索引擎 `不应该` 抓取 `当前链接` |
| follow | 搜索引擎 `应该` 抓取 `相关链接` |
| nofollow | 搜索引擎 `不应该` 抓取 `相关链接` 并记录权重 |

## 真假首页

### 是什么

```
https://juejin.im/
https://www.juejin.im/
```

对于`用户`来说这两个链接都是掘金的首页，可是对于 `搜索引擎` 来说这两个链接分别对应的是两个不同的网站。

### 为什么

在搜索引擎里，包括`参数`的不同，只有链接完全一样，才会认为是同一个链接。内容相似很有可能被`搜索引擎`判读为作弊，并且会导致权重被分散掉。就好比一条街上开两家 `万达广场` 直接会把客源稀释成两部分。

> 更多 URL 相关可以阅读 [URL 大爆炸](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/url.md)。

### 重定向

![金拱门](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/hyperlink/mcdonalds.png)

喜欢动手的同学可能会去试试访问 `https://www.juejin.im/`，就会发现链接会被重定向到 `https://juejin.im/`，确实这个方法便能帮助掘金主页从两个入口变为一个。但是细心的同学还会打开 `控制台` 发现跳转的 `HTTP Status Code` 为 `301` 而不是 `302`，这是为什么呢？

> ps: 小二没收一分钱广告费哦，只是单纯的举例子。

#### 301 状态码

301 (Permanently Moved)顾名思义指的是`永久性转移`，`搜索引擎`读取到 `301 状态码`时候会把跳转后的网站当做真正的链接，这样多个链接都会被当做同一个链接权重也得到了保持。使用的场景：

* 域名改变，告诉`搜索引擎`新域名和对新的域名进行收录。
* 短链接，利用短链接来方便分享`不利于记忆`和`过长`的原链接。
* 网页扩展名改变，有的站点在链接会带上 `.php`、`.html`、`.aspx`，当`用户`保存链接为书签和`搜索引擎`收录后，重新更改网页扩展名会导致原链接失效显示为 `404 Not Found`，访问流量白白流逝。
* 确认主页，就如开头给出的两个掘金主页链接，告诉`搜索引擎`哪个才是需要收录。

#### 302 状态码

302 Found（Moved Temporarily ）表示的是暂时性的转移，由于是`暂时性`的转移`搜索引擎`和人不一样不能做到精确的分辨出哪个才是该收录的。使用的场景：

* 页面刷新跳转，例如创建发布文章后，跳转到文章的发布页面。
* 回到原先页面，例如未登录前先使用302重定向到登录页面，登录成功后再跳回到原来请求的页面。
* 移动端和PC端，例如在手机访问 `https://juejin.im/` 跳转到 `https://m.juejin.im/`，不过有的公司用的是 301，最好还是做成响应式的网站。

注意：`搜索引擎` 有可能就会把跳转后的网站归结为是原网址的内容，比如 `baidu.com` 跳转到 `juejin.im` 可能会把掘金的内容归结为百度的，这也叫做 `网址劫持`。最简单的例子就是超市里的 `康师傅` 和 `康帅傅`：

![康师傅](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/hyperlink/noodles.png)

> ps: 小二真真真的没收一分钱广告费哦，只是单纯的举例子。

### 利用 html 标签

```
https://pushme.top/index.html?from=juejin
https://pushme.top/index.html?from=baidu
https://pushme.top/index.html?from=taobao
```

在为什么里提到了 `参数` 的不一样也会被当做不同链接，这里的三个链接其实都是主页，只不过是利用了 `from` 来判断用户的来源，可以利用 `rel="cononical"` 来告诉`搜索引擎`这几个链接都是表示哪个链接。

```
<link rel="cononical" href="https://pushme.top/index.html" />
```

当然上面 302 状态码中提到的 `移动端和PC端` 也可以用 `rel="cononical"` 和 `rel="alternate"` 来帮助`搜索引擎`理解两个网站的关系：

```html
<!--PC页面用 alternate 指向移动页面-->
<link rel="alternate" href="http://m.abc.com/">

<!--移动页面用 canonical 指向PC页面-->
<link rel="canonical" href="http://www.abc.com/">
```

> `rel="alternate"` 还可以用来实现网站的 `换肤功能`，本文主要是讲 SEO 相关就不扩展更多了。

## SEO 相关内容

* [H1 の 小秘密](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/heading.md)
* [SEO 初体验](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/seo-101.md)
* [img の 小九九](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/img-tag.md)
* [千里姻缘一线牵](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/hyperlink.md)
* [投怀送抱](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/sitemap.md)
* [漫游器法则](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/robot-txt.md)

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)