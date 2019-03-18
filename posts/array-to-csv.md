# 数组转 CSV 表格数据

## 简介

> [一天 30 秒 ⏱ 一段代码 ✍️ 一个场景 🖼](https://github.com/pushmetop/30-seconds-for-everyday)

将一个数组转化为逗号为分割符的字符串（CSV）即表格数据。

```javascript
// 该源码来自于 https://30secondsofcode.org
const arrayToCSV = (arr, delimiter = ',') =>
  arr.map(v => v.map(x => `"${x}"`).join(delimiter)).join('\n')
```

<!--more-->

## 代码分析

这个代码利用了 `Array.prototype.map()` 和 `Array.prototype.join()` 两个函数，实现了一个简单的数组转化为 csv 文件类型的代码。分别对代码进行两次遍历，第一层是遍历整个数组的项目，并在项目尾部添加换行符。第二层遍历为遍历数据行的值，并添加分隔符（分隔符定义时默认值为 `,`）。

## 使用场景

将页面上用户数据导出为 Excel 表格，并且提供下载。

```html  
<a id="download-user-data"
    onclick="downloadUserData(this)"
    download="downlaod.csv"
    href="#">download</a>      
```

```javascript
const title = [
    '姓名', '年龄', '性别'
]

const users = [
    { name: 'xiaoer', age: 24, sex: '男' },
    { name: 'xiaosi', age: 8, sex: '男' },
    { name: 'menty', age: 18, sex: '女' },
]

function downloadUserData(target) {
    const data = [
        title,
        ...(users.map((i) => [ i.name, i.age, i.sex ])),
    ]

    const csv = arrayToCSV(data)
    target.href = `data:text/csv;charset=utf-8,\ufeff${csv}`
}
```

## 打赏&联系

如果您感觉有收获，欢迎给我打赏，以激励我输出更多的优质内容。

![打赏&联系](https://raw.githubusercontent.com/pushmetop/resource/master/donate/donate.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)