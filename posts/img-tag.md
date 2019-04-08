<!-- # img の 小九九 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/img-tag/poster.png)

## 简介

> SEO、跨域、无障碍阅读、事件、图片标签

`小九九` 最直接的联想便是 `九九乘法表`，但是 `小九九` 也用在形容一个人在心里打着算盘 `小主意` 和 `小秘密`。小秘密已经被 [H1 の 小秘密](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/heading.md) 这篇文章使用了，为了体现小二的“博学多才”就换个词语吧（其实想个词脑袋已经💥爆炸了）。

开发中经常使用的 `<img>` 瞒着你许多事情，为了防止`青青草原`尴尬事件一起化身名侦探对其大探秘，看它到底有多少`小九九`！

> 主要讨论 `img 标签` 相关内容，关于图片的懒加载等优化操作并不在这展开。

## alt 属性

小二在刚开始学习 HTML 的时候只会用到 `<img>` 的 src 属性，觉得 `alt 属性` 并没有什么用写起来占位置还看着不舒服。但是 `alt 属性` 并没有想象中的那么简单哦。

### 占位

为什么会觉得 `alt 属性` 可有可无呢？因为 `alt 属性` 在下面这些情况才会显示出来：

* 网速太慢
* 浏览器禁用图像
* src 属性中的错误
* 网络原因加载不到图片
* 用户使用的是屏幕阅读器

可是平时很少会遇到这些情况并不高，所以也就没有感受到这个作用。正所谓的`失去的时候，才知道要珍惜`。
有的同学说：鼠标放到图片上的时候也会显示 `alt 属性` 中的内容。小二印象中也是这样的，可是写了个 demo 在 chrome 和 safari 都试过了放了半天都没有显示出来，不知道是不是现在浏览器都不支持这个了。

> IE 是前端程序 🐒 绕不过去的一个坎。

后来查询了一下才知道 `Internet Explorer` 才会显示，果然 `IE` 在浏览器中是独一档。而另外一档的浏览器都是按照 `alt 属性` 的标准来实现，只有图片加载不出时才显示。除了这个 `IE` 在 `<img>` 还有一些独一档的表现，小二还是把它绕过去吧。

### SEO

在 `SEO`（搜索引擎优化）方面 `alt 属性` 也有一定的作用哦，虽然现在有了 `AI` 可以识别出图片里面的内容是什么。可是搜索引擎并没有那么聪明哦，它在理解一张图片是什么的时候会去读取 `alt 属性`，并且配合页面的 title、description 来组织和保存这张图片的信息。这也是为什么在`百度`、`谷歌` 搜索关键词时能得到那么多相关图片的原因。

> 更多 SEO 相关知识可以阅读 [SEO初体验](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/seo-101.md) 和 [H1 の 小秘密](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/heading.md)。

### 特殊群体

对于盲人或者其他视力有障碍群体时可能看不到图片，他们可以通过屏幕阅读器等辅助工具阅读`alt 属性` 来理解图片内容。不过也不是所有图片都要加上 `alt 属性`，当装饰性和无意义的图片应该把 `alt 属性` 置为`空` 防止特殊群体对页面内容产生困惑。


> 希望大家都能加上 `alt 属性` 毕竟感受不到色彩和世界美妙时，还能感受图片的内容和温度。想想自己的代码能让世界更美好了，不是一件值得开心的事情吗？

> 更多 无障碍阅读 相关知识可以阅读 [H1 の 小秘密](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/heading.md)。

## 塌陷

在浏览网页经常会遇到 `图片` 突然加载出来，导致页面闪烁和图片闪现很影响体验。这是因为图片还未加载出来并且没有被设置`宽高` 时，浏览器不知道这个图片到底该怎么排布和渲染它。可以利用占位图片或者设置宽高来解决这个问题，也可以使用专门解决占位的库这里推荐 `Semantic UI` 的 `placeholder` 组件好用、好看。

> 更多内容可以查阅 [浏览器渲染流程](https://juejin.im/search?query=浏览器渲染&type=all)。

## 事件

图片也有着自己的事件：

| 事件 | 描述 |
| --- | --- |
| onabort | 当用户放弃图像的加载时调用。|
| onerror | 在加载图像的过程中发生错误时调用。|
| onload | 当图像加载完毕时调用件。|

不过这三个事件并不能获取到服务端返回相关的信息，利用这三个事件可以做到：

* 当用户放弃图片装载 和 图片加载失败的时候，可以调用占位图片来解决页面排版的问题。
* 当图片正在加载时可以显示占位图片或者动画效果，当加载成功时关闭占位相关内容。
* 当图片加载失败的时候重新请求图片或者给出提示。

## 相关操作

利用 `Image` 对象来获取并生成 DOM，并且利用了 `crossOrigin` 属性来允许跨域：

```javascript
const urlToImgDOM = ({ url, alt = '' }) => new Promise((reslove, reject) => {
    let imgDOM = new Image();
    
    imgDOM.alt = alt;
    imgDOM.setAttribute("crossOrigin", 'Anonymous');
    
    imgDOM.onload = () => reslove(imgDOM);
    imgDOM.onerror = () => reject(err);
    
    // 如果图片在浏览器缓存中
    // 会不除非 onload 函数需要后置
    imgDOM.src = url;
})
```

利用 DOM 来生成 canvas：

```javascript
const imgDOMToCanvas = (imgDom) => {
    // 创建 Canvas 画布
    let canvas = document.createElement("canvas");
    canvas.width = imgDom.width;
    canvas.height = imgDom.height;
    
    // 绘制图片
    let ctx = canvas.getContext('2d');
    ctx.drawImage(imgDom, 0, 0, canvas.width, canvas.height);

    return canvas;
}
```

利用 canvas 转 base64，注意图片要是跨域了会报错：

```
canvas.toDataURL()
```

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