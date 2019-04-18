<!-- # 无障碍工具 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/a11y-tools/poster.png)

## 前言

> 无障碍、工具、插件、a11y、Accessibility

其实 `无障碍` 离我们挺近的例如：

* 色盲：男生患有的比例为 `1/12`，女生患有的比例为 `1/200`。
* 老年人：看不清字需要使用放大镜、视觉灵敏度降低需要对比度太低的内容看不清。
* 孕妇：抱着小孩不能双手进行操作。

在编码和设计的时可以对这部分人群做出相应的帮助，对于无障碍设计方面可以看看下面这篇文章[无障碍设计](https://zhuanlan.zhihu.com/p/31657525) 非常详细，下面也给出一些用于无障碍开发的相关工具。

> 更多内容可以阅读 [无障碍世界](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/a11y-101.md)

## 工具

### WAI-ARIA

在上一篇文章 [HTML Cosplay](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/a11y-aria.md) 已经对 WAI-ARIA 有了一定的了解，其实 [WAI-ARIA](https://www.w3.org/TR/wai-aria-1.1/) 与前端开发并不冲突，你也可以把它当做开发的一个工具。例如在开发一个前端的按钮时：

```html
<style>
    .button {}
    .button.pressed {}
</style>

<!-- 按钮 -->
<div class="button">
    我是一个按钮
</div>

<!-- 按钮被激活 -->
<div class="button pressed">
    我是一个按钮
</div>
```

用上 `WAI-ARIA` 的 `aria-pressed` 来替代 `pressed` 还增加了按钮的语义：

```html
<style>
    .button {}
    .button[aria-pressed="true"] {}
</style>

<!-- 按钮 -->
<div class="button"
    role="button"
    aria-pressed="false">
    我是一个按钮
</div>

<!-- 按钮被激活 -->
<div class="button"
    role="button"
    aria-pressed="true">
    我是一个按钮
</div>
```

### 系统自带

* Mac：打开 `系统偏好设置>辅助功能` 即可选择视觉、听觉、交互相关的帮助工具，例如放大镜、色彩反转、对比度设置等等。
* iPhone：打开 `设置>通用>辅助功能` 即可选择视觉、听觉、交互相关的帮助工具，例如放大镜、色彩反转、对比度设置等等。
* 原生安卓在这方面做得好像比较好，小二手头只有一部 `oppo r9` 并没有比较实用的辅助工具。
* Win：小二没有使用 Win，欢迎大家到 Github 上帮助补充这部分内容。

### VoiceOver

一款苹果公司出品的无障碍辅助工具，内置于 Mac 电脑和 iPhone、iPad 等设备中。对于 Mac 电脑的使用在[语义化与无障碍树](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/a11y-tree.md)中已经有提到过，这里给出几个能流利使用的快捷键：

* `control+option+右箭头/左箭头`：切换导航，相当于焦点中的 `tab`。
* `control+option+shift+下箭头/上箭头`：进入或退出当前导航选中的内容。
* `control+option+command+h`：阅读网页内容中的 `heading`。
* `control+option+space`：模拟鼠标点击事件。
* `control+option+u`：使用转子。

对于 iPhone 和 iPad 快捷键：

* 单指轻点一次：选择项目。
* 单指轻点两次：模拟点击项目。
* 单指左右滑动：切换项目。
* 双指点击：停止阅读。
* 双指旋转：选择切换模式，只浏览链接、heading 等。
* 三指上下滑动：进行滚动或翻页。

### Chrome Accessibility

在 [语义化与无障碍树](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/a11y-tree.md) 中提到过这是谷歌浏览器自带的一个功能，当你在控制台 `Elements` 下选择节点或者审查元素的时候会给出 `无障碍树` 的相关内容：

![无障碍树](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/a11y-tools/tree.png)

在 `Audits` 中也增加了 `Accessibility` 的选项：

![审计](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/a11y-tools/audits.png)

当点击 `Run audits` 谷歌浏览器会给出当前页面无障碍相关的`评分`和`可优化`的地方而且内容十分详细：

![审计结果](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/a11y-tools/audits-result.png)

在 `Color Contrast Is Satisfactory` 中还可以看到当前页面对于 `颜色的建议`，当然也可以在 `Elements` 中直接点击颜色：

![颜色](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/a11y-tools/color.png)

在上面图片中可以看到，给出了两条对比曲线可以提供`选择`，并且给出了相应的`评分`，当然这只是作为一个参考并不是强制要求当做教条来使用。

### NoCoffee

一款谷歌浏览器插件使用后可以模拟 `色盲用户` 访问页面的效果，帮助我们找出页面中需要改进的地方。例如在掘金主页选择`绿色盲模拟`：

![绿色色盲](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/a11y-tools/blindness.png)

可以很清楚的看出掘金的 `蓝色系` 统统变成了 `紫色系`，对于红色的重点内容被变为了 `黄色`。

### High Contrast

一款谷歌浏览器插件使用后可以提高页面的 `对比度` 模拟 `颜色不敏感` 用户访问页面的效果，帮助我们找出页面中需要改进的地方。例如在掘金主页：

![对比度工具](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/a11y-tools/black.png)

## 无障碍相关内容

* [H1 の 小秘密](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/heading.md)
* [img の 小九九](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/img-tag.md)
* [无障碍世界](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/a11y-101.md)
* [扼住焦点的喉咙](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/a11y-foucs.md)
* [语义化与无障碍树](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/a11y-tree.md)
* [HTML Cosplay](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/a11y-aria.md)
* [无障碍工具](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/a11y-tools.md)

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。
* 如果您想与小二更多交流添加微信 `m353839115`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)