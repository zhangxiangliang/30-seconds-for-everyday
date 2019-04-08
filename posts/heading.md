<!-- # H1 の 小秘密 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/heading/poster.png)

## 简介

> heading 标签、SEO、无障碍阅读

> ps: 内容有点多，本来只想讲一个点，但是关联性太强了，所以辛苦大家了。

在学习 HTML 标签的时候，很多教程只告诉你 `怎么用` 而没有讲清楚 `是什么`，让我们一起从 `h1` 到 `h6` 开始重新认识 HTML 标签完善知识体系。

## 观其形

`Heading 标签` 指的就是网页中的 `h1` 到 `h6` 标签，很多同学最基本的认知就是 `h1` 到 `h6` 标签字体从大到小。那你有想过既然只是从大到小，那为什么不直接使用 `<h style="font-size:32px">` 这样的表现形式呢？

> 爱思考的同学会说：“可能是为了方便使用吧？”

乍一听好像挺有道理的，但是翻阅超多网站都使用的 `bootstrap` 源码 [scss/_type.scss](https://github.com/twbs/bootstrap/blob/ff29c1224c20b8fcf2d1e7c28426470f1dc3e40d/scss/_type.scss) 会看到在 `3到26 行` 对标题重新定义了样式：

```scss
//
// Headings
//

h1, h2, h3, h4, h5, h6,
.h1, .h2, .h3, .h4, .h5, .h6 {
  margin-bottom: $headings-margin-bottom;
  font-family: $headings-font-family;
  font-weight: $headings-font-weight;
  line-height: $headings-line-height;
  color: $headings-color;
}

h1, .h1 { @include font-size($h1-font-size); }
h2, .h2 { @include font-size($h2-font-size); }
h3, .h3 { @include font-size($h3-font-size); }
h4, .h4 { @include font-size($h4-font-size); }
h5, .h5 { @include font-size($h5-font-size); }
h6, .h6 { @include font-size($h6-font-size); }

.lead {
  @include font-size($lead-font-size);
  font-weight: $lead-font-weight;
}
```

在这段 scss 代码中，可以看到除了对 `h1` 到 `h6` 被重新定义外，还定义了对应的 `.h1` 到 `.h6` 类样式。这下带来了新的问题：

* 开发中经常会重置 `Heading 标签` 样式，那浏览器定义的默认样式岂不是多此一举？
* 只是为了方便使用，那 `boostrap` 还要再定义对应的 `.h1` 到 `.h6` 类样式？

## 知其意

在 1991 年，蒂姆·伯纳斯·李首次提出 `HTML` 的时候，并没有给页面添加样式的方法。如何显示页面是由浏览器决定的，用户也可以通过偏好设置来修改。这就好比现在最经常使用的 `markdown` 一样，使用一样的语法但是根据不同的设置，可以展示不一样的字体。

> 在报纸排版中往往会把`头条内容`加大字号表示重点，并通过其他`小字号`和`页面排版`来组织内容结构。

那面对密密麻麻没`样式`的网页时该怎么区分页面结构呢？参考报纸可以利用 `Heading 标签` 来组装页面形式，通过 `Heading 标签` 可以很方便的知道整个页面的结构：

* h1 用来修饰网页的主标题，一般是网页的标题，文章标题。
* h2 表示一个段落的标题，或者说副标题。
* h3 表示段落的小节标题。
* h4 到 h6 表示一些不重要的内容，用来做结构区分。

另外一个形象的例子就是 `markdown` 中的 `#` ~ `#####` 表示标题，我们甚至可以只看 `markdown` 不需要页面渲染就能读懂文章。这也是 `markdown` 设计的初衷：`方便书写和阅读`。

通过 `Heading 标签` 浏览器可以很容易的读出整个页面的主题结构，甚至可以生成目录方便用户阅读，在没有样式的时候还是相当有用的，当然随着 `CSS` 的诞生页面样式可以更好的组织，很多同学也就忘记了它的本意。

> 小练习：遍历 dom 节点通过 Heading 标签来生成一个网页目录。

## 小蜘蛛

> 廉颇老矣，尚能饭否。

现在很多同学都是使用 `<div>` 和 `<span>` 来组织页面结构，已经不去在意 `Heading 标签` 带来的意义了。除了 `Heading 标签` 在 HTML5 也带来了更多语义化的标签，来帮助我们组织页面结构。

在 `SEO` （搜索引擎优化）时，`小蜘蛛` 爬取页面结构时还是会用到这些语义化和结构 来了解页面信息。毕竟`小蜘蛛`并不是人能读懂页面，它们只能按照既定的规则来读取。打开掘金的一篇文章[小姐姐的诱惑](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/hijack.md)，`控制台`选择`文章标题` 便能看到使用的是 h1 标签：

![页面标题](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/heading/title.png)

通过 `h1` 组织页面结构告诉 `小蜘蛛` 这个页面的标题是什么，`小蜘蛛`也会把这个存储起来，当在搜索引擎搜索 `小姐姐的诱惑` 等相关词语时，就能找到这篇文章啦。当然在页面右侧变是文章目录：

![文章目录](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/heading/contents.png)

是不是非常方便我们查看文章结构，进行内容的跳转呢？

> SEO 指的是搜索引擎优化，简单来讲就是怎么让 `百度` 和 `谷歌` 更容易理解你的网站并对齐进行排序。

## 特殊群体

除了小蜘蛛外使用 `Heading 标签` 还能方便特殊群体，最著名的人之一便是 `霍金` 大大了。`霍金` 大大只有两个手指头，如果他要浏览网页该怎么办呢？

其实现在有很多帮助特殊群体的软件，例如浏览器中的无障碍模式。这些软件通过解析页面的结构来帮组特殊群体用户来操作页面。例如`列出页面目录`方便特殊群体用户选择，`读出页面目录`帮助 视力障碍人士 方便选着和使用网页。

如果大家都一味的使用 `<div>` 和 `<span>` 特殊群体用户只能一个个 `dom` 节点听过去了，大家感兴趣可以打开`无障碍模式`试试看。`iPhone` 用户最常用的 `辅助控制器` 其实是设计给`特殊群体`使用的：

![辅助控制器](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/heading/iphone.png)

可以看到 `自定义` 中可以模拟 `缩放` 和 `三维粗触控` 等操作，这样像`霍金`大大也可以使用`iPhone`进行缩放等特殊操作了，送上一句`霍金`大大的名言：

> 永恒是很长的时间，特别是对尽头而言。 --by 霍金（这次不是鲁迅了）

## 填坑

现在解决了为什么使用 `Heading 标签`，那为什么 `bootstrap` 中还定义了 `.h1` 到 `.h6` 标签呢？其实问题的答案已经很明了：

* 真真正正的在使用字体样式。
* 不破坏 `Heading 标签` 的语义，使得造成误解。

## 希望

如果大家在开发的时候不是只`面向企业`或者 `自己使用`，希望大家能尽量使用 `Heading 标签` 和 `语义化标签`，除了能带来 `SEO` 上的帮助还能帮助`特殊群体` 何乐而不为呢？

## SEO 相关内容

* [H1 の 小秘密](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/heading.md)
* [SEO 初体验](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/seo-101.md)
* [img の 小九九](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/img-tag.md)
* [千里姻缘一线牵](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/hyperlink.md)

## 一起成长

> 👇 更新平台多偶尔会漏掉，如果觉得文章还行点个 `star` 防走失。

如果您感觉有收获可以点赞关注`激励我`，也欢迎到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 加个 star。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)