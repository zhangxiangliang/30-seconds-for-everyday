<!-- # HTML Cosplay -->

![封面](../images/a11y-aria/poster.png)

## 简介

> 无障碍、WAI、ARIA、a11y、Accessibility、框架选择

如何向 `视障用户` 介绍兔子长什么样？有的同学可能会说：

* 毛茸茸的长耳朵。
* 短短圆圆的小尾巴。
* 红红的眼睛。

那如何向 `视障用户` 介绍网页长什么样？有看过 [语义化与无障碍树](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/a11y-tree.md) 的同学可能会说：

* header 标签表示一个网页的页眉。
* main 标签表示一个网页的内容。
* footer 标签表示一个网页的页脚。

`哎呦不错哦~` 那你给我表演一下怎么描述 `导航` 呢？

## 导航

### 现在

在 HTML5 语义化标签的加持下导航可以这样写：

```html
<nav>
    <a href="home">主页</a>
    <a href="users">用户</a>
</nav>
```

不同用户理解：

* 普通用户通过 `显示效果` 识别出是导航。
* 程序员通过 `nav 标签` 识别出是导航。
* 视障用户通过 `屏幕阅读器` 识别出是导航。

### 过去

这个时候有同学想过在 `<nav>` 标签还没有出现的时候，只靠 `div` 和 `span` 标签一把梭是时候怎么写的？

```html
<div class="navigation">
    <a href="home">主页</a>
    <a href="users">用户</a>
</div>
```

不同用户理解：

* 普通用户通过 `显示效果` 识别出是导航。
* 程序员通过 `class="navigation"` 识别出是导航。
* 视障用户通过 `屏幕阅读器` 识别出是两个链接。

这对于 `视障用户` 多么不友好，他们除了知道有两个链接并不能识别出是导航。

### Cosplay

聪明的同学肯定想到了：
 
* 是否可以指定一个规范？
* 是否可以通过 `cosplay` 来把 `div 标签` 变成 `nav 标签`？

确实存在一个规范叫做 `Web Accessibility Initiative - Accessible Rich Internet Applications` 缩写 WAI-ARIA，它的作用就和同学们想到的一样通过角色扮演来描述 `html` 使得 `视力障碍` 用户可以理解 `html` 所表达的含义。

使用 `WAI-ARIA` 来表单 `nav 标签`，屏幕阅读器便会帮助`视障用户`识别出是导航 ：

```html
<div class="navigation" role="navigation">
    <a href="home">主页</a>
    <a href="users">用户</a>
</div>
```

### 好奇宝宝

好奇宝宝肯定会问：可是有的页面有 `主导航` 和 `副导航` 甚至还有 `面包屑导航`、`奇奇怪怪不知道什么的导航` 正常用户可以通过视觉秒理解是什么，那视障用户怎么办呢？

居然能想到这么厉害的问题，不过没关系 `WAI-ARIA` 已经定义好了通过 `aria-label` 标签来描述是什么：

```html
<div class="navigation"
    role="navigation"
    aria-label="主导航">
    <a href="home">主页</a>
    <a href="users">用户</a>
</div>
<div class="navigation"
    role="navigation"
    aria-label="奇奇怪怪不知道什么的导航">
    <a href="sister">小姐姐</a>
    <a href="brother">小哥哥</a>
</div>
```


## WAI-ARIA

可能还是有同学不是很能理解 `WAI-ARIA` 是什么，简单来说 `WAI-ARIA` 便是视障用户的 `UI`：

| 用户 | 兔子 | 页面 |
| --- | --- | --- |
| 普通用户 | 看到兔子样子 | 看到页面效果 |
| 视障用户 | 知道兔子构成 | 知道页面构成 |


通过上面的`导航`例子也大概知道了 `WAI-ARIA` 的使用方法，但是 `WAI-ARIA` 并没有这么简单，它其实定义了一系列的属性和角色来帮助 `视力障碍` 用户理解页面，只不过导航的结构比较简单，如果像是复杂一点的 `多项选择` 除了要使用 `WAI-ARIA` 规定的标签，还有实现 `WAI-ARIA` 规定的 `焦点`、`键盘事件` 等。

更多内容可以阅读 [WAI-ARIA](https://www.w3.org/TR/wai-aria-1.1/) 这份文档算是详细描述了所有的规则，如果觉得复杂可以阅读 [WAI-ARIA 实践](https://www.w3.org/TR/wai-aria-practices/)，如果觉得英语看不来可以阅读 [饿了么前端团队翻译的 WAI-ARIA 实践](https://elemefe.github.io/WAI-ARIA-Practices/#/)。

## 题外话

### 关于学习

有的人很奇怪对事物的认识取决于第一次，比如小二先接触的 `LOL` 后面玩 `DotA` 对正反补兵很不适应。所以在小二看来应该在学习 HTML 的时候应该穿插部分 `WAI-ARIA` 内容，在学习部分 `JavaScript` 后应该穿插实现几个 `WAI-ARIA` 规定的角色，当然现在学习也不迟。

### 现实情况

如果大家有追更`小二`就会记得：

* [扼住焦点的喉咙](https://juejin.im/post/5cb03013e51d456e7349dbde#heading-18) 挑选框架时提到的 `Element UI` 部分语义化做的还不错。

* 如果你真的点进去上文提到的 [饿了么前端团队翻译的 WAI-ARIA 实践](https://elemefe.github.io/WAI-ARIA-Practices/#/) 你就会发现：这个项目停止在了 `2018年7月26日` 而且没有完全翻译完。

可能是因为某些原因导致的，但是通过阅读 [饿了么前端团队翻译的 WAI-ARIA 实践](https://elemefe.github.io/WAI-ARIA-Practices/#/) 在每篇文章底部 `Example` 中重复出现 `Material` 和 `Element`，小二个人能感受到的是翻译这篇文章和写相关代码同学对帮助 `无障碍群体`的热情。

社会挺现实的大家都`忙忙碌碌`、`加班赚钱`有很多需要的事情要去做`小二也不例外`，无障碍可能是个遥远的话题。小二这几篇文章也只能是帮大家认识一下这个群体和给出相关的知识，本来还想讲一下 `无障碍视觉设计` 相关内容，但是 `鱼头哥哥` 最近分享了几篇相关文章都挺好的。

### 期望

* 如果可以使用 `heading` 和 语义化、图片加上 `alt` 也挺好。
* 如果还可以选择一个无障碍做得好的框架，比如二哲哥哥常说的 `material ui`。
* 如果挺可以选择阅读 `material ui` 源码和 [WAI-ARIA](https://www.w3.org/TR/wai-aria-1.1/)。
* 最后希望鱼头哥哥的 `无障碍世界` 可以实现。

## 无障碍相关内容

* [H1 の 小秘密](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/heading.md)
* [img の 小九九](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/img-tag.md)
* [无障碍世界](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/a11y-101.md)
* [扼住焦点的喉咙](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/a11y-foucs.md)
* [语义化与无障碍树](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/a11y-tree.md)
* [HTML Cosplay](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/a11y-aria.md)
* [无障碍工具](https://github.com/zhangxiangliang/30-seconds-for-everyday/blob/master/posts/a11y-tools.md)

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/zhangxiangliang/30-seconds-for-everyday) 给个 `小星星`。

> 本文原稿来自 [ZhangXiangLiang](https://github.com/zhangxiangliang)
