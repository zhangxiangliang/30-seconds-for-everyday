<!-- # 小姐姐的诱惑 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/hijack/poster.png)

## 简介

> hijack、点击劫持、安全、注入攻击、CSRF

老板今天有 `刘备` 嘛？这是某个业内黑话，小二来给你解释解释：刘备一直称自己是中山靖王的后代，在曹操把刘备带到朝廷后，汉献帝为了拉拢他，才认他为皇叔，确认了他的身份，简称刘皇(黄)叔(书)。

不少成年雄性 🐒 常常会漫游在`黄色`丛林中采摘`果实`，食用完毕后往往会发现 QQ 空间被自动发送了状态等`灵异事件`，吓得赶紧群发 `账号被盗了，大家不要相信` 证明自己真身，其实在除了黄色丛林很多网址都暗藏着不少“危险”。

## iframe

在日常使用网站的时候经常会记录登录状态，方便下次使用不需要输入密码，如果可以用`某些方法`模拟用户自己打开了网页，是不是也可以在用户`不知情`的情况下进行`关注`和`发文`等操作。一个老旧的 html 标签 `iframe` 便拥有这个功能，例如嵌入百度贴吧页面：

```html
<iframe src="http://tieba.baidu.com" style="width: 100%;height:100vh"></iframe>
```

## 勾搭小姐姐

如果你在本地登录过贴吧，这个时候你便会看到页面里的 `iframe` 打开了百度贴吧的页面并且你还登录了，如果这个时候在页面上进行点击关注等操作也会成功。你可能会说我又不笨怎么可能会自己去点击呢？

那如果这个时候 `iframe` 被设置成透明你还看得出来嘛？再加个诱导你的按钮 `勾搭小姐姐` 重叠在贴吧点击关注，你这个时候点击了 `勾搭小姐姐` 是不是就会关注了某个贴吧用户了。这种攻击方法叫做 `点击劫持` 是不是很形象，利用透明 iframe 劫持了你的点击操作。

## 凶狠小姐姐

这里只是简单介绍了一下 `点击劫持` 的概念，如果去调用一些危险操作的页面（转账，付款，重置密码，注销账号），在开通小额免密支付的情况下，也许会在完全不知情的情况带来很多损失。

它还能配合一些其他攻击完成更复杂的操作，比如之前 [大家一起被捕吧](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/lets-get-arrested.md) 提到的 `JavaScript 注入攻击` 也可以配合 `点击劫持` 和 `复制黏贴`，来诱导你进行文本输入并提交文本到`被攻击站点`。甚至可以利用 `iframe` 来做到绕过 `CSRF` 进行对站点进行攻击，这些安全相关的知识感兴趣大家可以自己查阅。

## 再见小姐姐

#### X-FRAME-OPTIONS

`X-FRAME-OPTIONS` 是微软提出的一个http头，专门用来防御利用iframe嵌套的点击劫持攻击。它有三个可选值：

| 值 | 解释 |
| --- | --- |
| DENY | 拒绝任何域加载 |
| SAMEORIGIN | 允许同源域下加载 |
| ALLOW-FROM | 可以定义允许frame加载的页面地址 |

关注小二的同学知道小二很喜欢泡在`掘金`，为什么这次举例是贴吧而不是 `掘金` 呢？因为掘金利用了 `X-FRAME-OPTIONS` 来防止自己被非同源网站 iframe 引入，不信你可以试试看。相信你也会得到和我一样的页面提示：

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/hijack/juejin.png)

#### 增加操作难度

既然 `点击劫持` 是利用了用户无意识的点击操作，可以增加用户的操作难度来让劫持变难。例如在高危险操作使用验证码，在面对存在验证码的页面时，用户看不到这个透明页面，肯定是不会输入验证码的，可以防止点击劫持造成危害。

#### 脚本防护

可以使用 JavaScript 代码防止被 iframe 嵌套，这种方法叫做 `frame busting`。例如判断上级 location 是不是与自己一样：

```javascript
if ( top.location != location ) {
    top.location = self.location;
}
```

不过这种方法很容易被绕过，比如使用 `iframe` 的 `sandbox` 的属性可以阻止被攻击网站执行脚本，或者多层嵌套的 `iframe`。

#### 改变自己

当然不是每个网站都会像 `掘金` 这样帮助我们防止 `点击劫持`，我们也可以改变自己来解决这个问题。最简单的方式告别小姐姐，从源头上解决被恶意的人盯上。

当然你如果离不开小姐姐可以给浏览器装上插件，例如谷歌浏览器的 `No-Script Suite Lite`，可以添加你信任的网址到白名单之中，其他网址将被禁止脚本等操作。

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)