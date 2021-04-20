<!-- # 发布与订阅 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/event/poster.png)

## 前言

> 设计模式、发布、订阅、Event、事件

今天分享一个开发中比较常用到的设计模式`发布-订阅模式`也可以叫`观察者模式`，在`发布-订阅模式`中主要有两个角色：发布者 和 订阅者。

生活中最常用到的一个场景就是当你在QQ空间发布一条心情的时候所有你的QQ好友都会收到你的QQ动态，在这个例子中 `你` 就是 `发布者`，而 `QQ 好友` 则会是订阅者。

```javascript
const createEventHub = () => ({
    hub: Object.create(null),

    emit(event, data) {
        (this.hub[event] || []).forEach(handler => handler(data));
    },

    on(event, handler) {
        if (!this.hub[event]) this.hub[event] = [];
        this.hub[event].push(handler);
    },

    off(event, handler) {
        const i = (this.hub[event] || []).findIndex(h => h === handler);
        if (i > -1) this.hub[event].splice(i, 1);
    }
});
```

<!-- more -->

## 代码分析

使用 `Object.prototype.create` 方法来快速创建了一个内部对象：

```javascript
hub: Object.create(null)
```

使用 `Array.prototype.forEach` 来遍历监听事件对应的所有操作：

```javascript
emit(event, data) {
    (this.hub[event] || []).forEach(handler => handler(data));
}
```

使用 `Array.prototype.push` 来存储事件对应的操作：

```javascript
on(event, handler) {
    if (!this.hub[event]) this.hub[event] = [];
    this.hub[event].push(handler);
}
```

使用 `Array.prototype.findIndex` 来查询事件对应的操作并使用 `Array.prototype.splice` 来去除操作：

```javascript
off(event, handler) {
    const i = (this.hub[event] || []).findIndex(h => h === handler);
    if (i > -1) this.hub[event].splice(i, 1);
}
```

## 使用场景

当用户输入 `表单数据` 对 `页面数据` 和 `data` 进行同步更新，反之当 `data` 被其他操作修改时 对 `页面数据` 和 `表单数据` 进行同步更新，这样就简单的实现了一个类似 `Vue` 的数据双向绑定。

记得在项目开发过程中 `大叔` 在一个 jQuery 的前端项目中为了方便数据的变更和维护引入了 `Vue` 使得项目变得臃肿和复杂，如果使用 `发布-订阅模式` 则可以很方便的来实现这个操作而无需引入这么大的一个框架。

当单页面项目并不巨大，我们无需引入像 `Redux` 和 `Vuex` 这样的数据管理库，使用 `发布-订阅模式` 也可以很方便的管理组件之间的数据变更和依赖更新。

##### 结构

```html
<h2>用户数据</h2>
<div id="info">
    <h3>
        用户名：<span id="username"></span>
    </h3>
    <h3>
        密码：<span id="password"></span>
    </h3>
</div>

<h2>请输入用户数据</h2>
<div id="form">
    <input type="text" name="username" oninput="hub.emit('oninput', 'username')" />
    <input type="text" name="password" oninput="hub.emit('oninput', 'password')" />
    <button type="button" onclick="hub.emit('submit')">确定</button>
    <button type="button" onclick="hub.emit('resetFormData')">重置</button>
</div>
```

##### 脚本
```javascript

// 基础表单数据
let data = {
    username: '',
    password: '',
}

const hub = createEventHub()

// 监听表单输入事件
hub.on('oninput', (name) => {
    const dom = document.querySelector(`[name="${name}"]`)
    hub.emit('setFormData', { name, value: dom.value })
})

// 监听数据变更事件
hub.on('setFormData', ({ name, value }) => {
    data[name] = value
})

// 监听数据变更事件
hub.on('setFormData', ({ name, value }) => {
    const dom = document.querySelector(`#${name}`)
    dom.innerHTML = value
})

// 监听数据变更事件
hub.on('setFormData', ({ name, value }) => {
    const dom = document.querySelector(`[name="${name}"]`)
    dom.value = value
})

// 监听页面数据提交事件
hub.on('submit', () => {
    // ajax 发送数据请
    // 这里用 setTimeout 来模拟 ajax 请求发送
    setTimeout(() => {
        alert('数据发送成功')
        hub.emit('resetFormData')
    }, 1000)
})

// 监听页面数据提交事件
hub.on('resetFormData', () => {
    hub.emit('setFormData', { name: 'username', value: '' })
    hub.emit('setFormData', { name: 'password', value: '' })
})
```

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)