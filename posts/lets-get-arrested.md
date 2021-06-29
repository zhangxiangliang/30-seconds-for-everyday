<!-- # 大家一起被捕吧 -->

![封面](../images/lets-get-arrested/poster.png)

## 简介

> 安全、注入攻击、XSS

> 13岁女学生被捕：因发布 JavaScript 无限循环代码。

这条新闻是来自 `2019年3月10日` 很多同学匆匆一瞥便滑动屏幕去看下一条消息了，并没有去了解这段代码是什么，怎么办才能防止这个问题。事情发生后为了抗议日本警察采取的行动和将此行为定为犯罪的荒谬做法，东京开发者 Kimikazu Kato 在 GitHub 上创建了一个名为 [`Let's Get Arrested（来逮捕我们）`](https://github.com/hamukazu/lets-get-arrested) 的仓库这也是本篇文章名的由来。

```javascript
for ( ; ; ) {
window.alert("　∧_∧　ババババ\n（ ・ω・)=つ≡つ\n（っ ≡つ=つ\n`/　　)\n(ノΠＵ\n何回閉じても無駄ですよ～ww\nm9（＾Д＾）プギャー！！\n　byソル (@0_Infinity_)")
}
```

## 是什么

女学生的这段代码专业点的叫法是 `JavaScript 注入攻击`。在日常开发中我们往往会从用户那获得各种输入，例如搜索框、评论框、文章内容等等。大家一般都默认用户会正常操作输入文本，可是你有没有想过用户也可以输入脚本，那么当页面渲染这些`脚本`时便会被执行。

女学生的这段代码只是简单的使用了 `alert` 和 `for(;;)` 来无限循环输出提示并不是算特别大的危害，使用 `JavaScript 注入攻击` 甚至可以窃取来自其他用户浏览器的 Cookies 值，如果其中的数据包含账号密码等敏感信息是很可怕的。

## 怎么办

`Vue.js` 官方文档在 [模板>插值>原始 HTML](https://cn.vuejs.org/v2/guide/syntax.html#%E5%8E%9F%E5%A7%8B-HTML) 中有下面这段话：

> 你的站点上动态渲染的任意 HTML 可能会非常危险，因为它很容易导致 XSS 攻击。请只对可信内容使用 HTML 插值，绝不要对用户提供的内容使用插值。

其实现在很多开发框架都帮我们做到了这点只是很多人并没有去思考为什么，`Vue.js` 在使用 `{{}}` 语法输出文本的时候 html 相关的标签中的 `<`、`>`、`'`、`"`、`&` 会被对应转化为 `&lt;`、`&gt;`、`&#39;`、`&quot;`、`&amp;` 来防止渲染内容时被 `JavaScript 注入攻击`。

那如果使用的框架并没有帮助实现这个函数时，可以利用正则和上述规则来实现一个转化 html 的小工具：

```javascript
const escapeHTML = str =>
    str.replace(/[&<>'"]/g, tag => ({
        '&': '&amp;',
        '<': '&lt;',
        '>': '&gt;',
        "'": '&#39;',
        '"': '&quot;'
    }[tag] || tag));
```

当然这里也给出恢复 html 的小工具：

```javascript
const unescapeHTML = str =>
    str.replace(/&amp;|&lt;|&gt;|&#39;|&quot;/g,tag => ({
        '&amp;': '&',
        '&lt;': '<',
        '&gt;': '>',
        '&#39;': "'",
        '&quot;': '"'
    }[tag] || tag));
```

除了前端输出时要进行处理，后端在存储和输出数据的时候也可以进行 html 的转换。

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/zhangxiangliang/30-seconds-for-everyday) 给个 `小星星`。

> 本文原稿来自 [ZhangXiangLiang](https://github.com/zhangxiangliang)