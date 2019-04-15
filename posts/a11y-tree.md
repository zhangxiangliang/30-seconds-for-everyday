<!-- # 语义化与无障碍树 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/a11y-tree/poster.png)

## 简介

> 无障碍、语义化、a11y、Accessibility、无障碍树

对于语义化出发点不一样观点也不一样：

* `SEO` 角度：原有的 heading、a、img 等标签加上新带来的标签，配合良好的结构和语义内容非常有帮助。
* `A前端` 角度：能够完成项目 `span、div` 一把梭美滋滋，为什么要语义化呢？
* `B前端` 角度：谁会阅读输出后的 `HTML` ，在项目开发中不使用 `语义化` 也可以写出结构漂亮的 `组件代码`。
* `其他` 角度：此处省略一万字。

## 什么是语义化

有的同学会说了：img、heading 也有语义化？其实语义化并不只是 HTML5 中新增加的 `<header>`、`<main>` 等标签，它们更多的算是结构语义化。

`图片语义化` 依靠着 `img` 标签中的 `alt` 和 `title` 属性，其中 `alt` 用于图片描述，这个描述是给搜索引擎和屏幕阅读器使用。并且当图片无法显示时，页面会显示alt中的文字。

`标题语义化` 包括了从 `h1` 到 `h6` 的标题，在没有 HTML5 新增加的结构标签时，更多的是由 `heading` 来表示页面的结构。

还有 `表格语义化` 包括 table、caption、thead、tbody、tfoot、th 标签，等等语义化相关标签就不在这里赘述了很多的文章都讲得非常好。

## 换位思考

> `一千个人眼里有一千个哈姆雷特`

多姿多彩的世界中也包括了一部分 `特殊群体`，其中也包括了 `盲人`、`弱视` 等群体。今天一起扮演一位 `视力障碍用户`，站在他的角度来看看这个 `互联网` 世界，小二使用的是 Mac 便用 VoiceOver 下面是常用快捷键：

* `control+option+右箭头/左箭头`：切换导航，相当于焦点中的 `tab`。
* `control+option+shift+下箭头/上箭头`：进入或退出当前导航选中的内容。
* `control+option+command+h`：阅读网页内容中的 `heading`。
* `control+option+space`：模拟鼠标点击事件。
* `control+option+u`：使用转子。

## 图片

### 入困境

从一张图片来了解 `盲人世界`，代码如下：

```html
<img src="https://user-gold-cdn.xitu.io/2019/4/11/16a0b73404feaca5">
```

显示的效果如下，作为正常用户可以很清楚的便理解了图片上的内容：

![土土相亲](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/a11y-tree/tutu.png)

而通过 `VoiceOver` 模拟盲人查看图片会得到这么一段语言：

```
16a0b73404feaca5, 图像
```

> `视障用户`：咦 `16a0b73404feaca5` 是什么呀？听不懂也理解不来。

### 出困境

这是因为没有给图片加上 `alt` 属性，导致 VoiceOver 在读取页面信息的时候只能去读取 `src` 最后一个斜杠后的内容`16a0b73404feaca5`，因为链接资源里最后的部分为它的文件名，解决的方法很简单加上 `alt` 属性描述。

```html
<img src="https://user-gold-cdn.xitu.io/2019/4/11/16a0b73404feaca5"
    alt="一只叫做土土的小猫咪相亲中，正在看一只漂亮的小猫咪。">
```

这个时候再使用 `VoiceOver` 模拟盲人查看图片会得到这么一段语言：

```
土土相亲中，正在看一只漂亮的小猫咪, 图像
```

> `视障用户`：哦哦，原来是小猫咪在相亲啊。

### 学习角度

看到这里又有不同的学习方式：

* 普通前端：写 img 要把 alt 属性也给带上。
* 有后端思维的前端：产品在做需求的时候，上传图片要补上 `图片描述字段`。
* 有丰富经验的前端：有些图片只是装饰并没有实际作用怎么办？

最后这个问题问得非常好：

* 不写上 `alt` 属性会被读取 `src` 中的文件名。
* 写上 `alt` 又会导致过多信息出现，使得视力障碍用户难以理解。
* 解决方法：将 `alt` 设置为 `空字符串`，这样屏幕阅读工具就会跳过它。

> 更多内容可以阅读 [img の 小九九](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/img-tag.md)

## Heading

在浏览网页的时候，正常用户可以通过鼠标滚动或者键盘的上下键。而视力障碍用户`看不到`网页内容，那通过什么来在网页内容搜索中上下滚动浏览页面呢？答案便是 `Heading` 国外的网站大多无障碍体验多做得比较好，毕竟在法律政策下必须做好 `无障碍体验`。这里选用谷歌搜索来演示 `Heading`  对视力障碍群体的帮助：

![谷歌搜索彭于晏](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/a11y-tree/pengyuyan.gif)

使用 `control+option+command+h` 在标题之间进行跳转，你会发现右下角分别显示着：

* 标题级别 1 无障碍功能链接。
* 标题级别 1 搜索模式。
* 标题级别 1 搜索结果。
* 标题级别 2 网络搜索结果。
* 彭于晏-维基百科，自由的百科全书 彭于晏，超级链接。
* 彭于晏_百度百科，彭于晏，超级链接。
* 更多内容就不描述了。

可以发现一开始的 4 个标题，都是在页面上`看不到`标题标签。这是谷歌搜索为视力障碍用户提供的页面锚点，方便视力障碍用在页面上通过 `heading` 跳转和浏览内容区域，接下来的几个标题便是利用 `heading` 配合 `a` 标签来实现搜索项目的浏览。

`heading` 的效果在页面上显而易见，视力障碍群体也可以很方便的浏览网页。

> 更多内容可以阅读 [H1 的小秘密](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/heading.md)

## label

### 入困境

标签也是在开发中经常被忽略的内容结构如下：

```html
<div class="row">
    用户名：<input type="text" name="username">
</div>
```

表单显示效果如下：

![输入用户名](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/a11y-tree/input.png)

作为正常用户看着没什么问题，可是作为视障用户在使用 `VoiceOver` 会听到：

```
编辑文本，空白
```

这下又让视障用户陷入沉思了，空白指的是什么？

### 出困境

这是因为没有给 input 配上指定 label，屏幕阅读器并不能很好的去识别 input 所表达的含义。

```html
<div class="row">
    <label for="username">用户名</label>
    <input type="text" name="username" id="username">
</div>

<label>
    <input type="text" name="address" id="address">
    用户地址
</label>
```

这个时候再使用 `VoiceOver` 模拟盲人查看会听到：

```
用户名，编辑文本，空白
用户地址，编辑文本，空白
```

这下盲人用户很容易就能理解表单信息。

## 结构语义化

再来看看结构语义化能带来的好处：

```html
<header>
    <div class="container">
        <h1>PushMeTop</h1>
        <nav>
            <a href="#">主页</a>
            <a href="#">文章</a>
            <a href="#">视频</a>
        </nav>
    </div>
</header>
<main>
    <div class="card">
        <form>
            <div class="row">
                <label for="username">用户名</label>
                <input type="text" name="username" id="username">
            </div>
            <div class="row">
                <label for="password">密码</label>
                <input type="password" name="password" id="password">
            </div>
            <div class="row">
                <button type="submit">登录</button>
            </div>
        </form>
    </div>
</main>
<footer>
    <div class="container">
        <div class="col-1">
            <a href="#">联系我们</a>
        </div>
        <div class="col-1">
            <a href="#">加入我们</a>
        </div>
    </div>
</footer>
```

在 `VoiceOver` 使用转子功能可以看到如下效果：

![转子](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/a11y-tree/tool.gif)

转子通过语义化标签，很轻松的便把网页的结构识别出来了。在`文章`功能下可以看到横幅、导航、主题内容、页脚 和他们内部相关的元素，而在 `地标` 中也可以通过 横幅、导航、主题内容快速浏览网页。

## 无障碍树

浏览器在渲染的时候会构建 DOM 树，而无障碍工具在理解页面的时候则通过 `无障碍树` 来让 `特殊群体` 理解页面。其实开发过程中离 `无障碍树` 相当近只不过大家一直都没有注意，打开控制台选择 `Accessibility` 即可看到：

![无障碍树](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/a11y-tree/console.png)

无障碍树的构建便是通过 `语义化` 来实现的，点开 banner、main、contentinfo 进行具体内容查看，而构成无障碍树节点由：Role, Name, State, Value 组成。

反映快的同学就会想到上面提到的 `用户名表单`：

* Name: 用户名
* Role: 编辑文本
* Value：空白
* State：无

当 `VoiceOver` 在阅读页面节点便会读出：

```
用户名，编辑文本，空白
```

这里只对`无障碍树`做一个简单的介绍，`无障碍树`和`语义化`关系紧密，细心的同学还会发现截图中 `WebArea` 的 `Name` 值中有出现 `aria-*` 相关字段，其实 `ARIA` 是能够让残障人士更加便利的访问 Web 内容和使用 Web 应用（特别是那些由 Ajax 和 JavaScript 开发的）的一套机制，对 `html` 标签的一个补充。

> 更多内容可以阅读 [ARIA - 无障碍](https://developer.mozilla.org/zh-CN/docs/Web/Accessibility/ARIA) 。

## 总结

其实被 KPI 和 需求的追赶下并不能很好的做到 `语义化`，这也是现实世界的无奈。本文着重讲了 `heading`、`img`、`label` 这些开发中最简单也是最触手可及的一些语义化，大家可以在开发时稍加使用，虽然不能做到百分比语义化，但是能提供到一部分的帮助也是挺好的。

最推荐的方式还是使用 `无障碍` 做得好的框架来开发，可以帮助我们快速的实现 `无障碍`，这里引用`二哲`的一句话：

> 无障碍我就服 `material ui`。

## 无障碍相关内容

* [H1 の 小秘密](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/heading.md)
* [img の 小九九](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/img-tag.md)
* [无障碍世界](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/a11y-101.md)
* [扼住焦点的喉咙](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/a11y-foucs.md)
* [语义化与无障碍树](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/a11y-tree.md)

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。
* 如果您想与小二更多交流添加微信 `m353839115`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)
