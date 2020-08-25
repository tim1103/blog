---
layout: post
title: '今日诗词 | 一个诗词一言API'
subtitle: ' 欲把西湖比西子，淡妆浓抹总相宜'
date: 2020-04-07
categories: 发现
cover: 'https://s1.ax1x.com/2020/08/11/aOwexg.png'
tags: 
---
先上官网:
[https://www.jinrishici.com/ ](https://www.jinrishici.com/)
官网长这样,一眼望去就是诗词:

![](https://s1.ax1x.com/2020/08/11/aOwexg.png)

调用很方便,稍微整理了下:


### HTML

在 HTML 中需要加载诗词的地方放置以下加载代码即可,和  **网站统计**  的安装方法一致。

```
<span id="jinrishici-sentence">正在加载今日诗词....</span>
<script src="https://sdk.jinrishici.com/v2/browser/jinrishici.js" charset="utf-8"></script>
```

SDK 会自动寻找  `id`  或者  `class`  为  `jinrishici-sentence`  的标签，将里面的内容替换为诗词

如果需要在多个地方显示诗词，添加多个 class="  `jinrishici-sentence`  " 的 span 即可

### 捷径/浏览器插件接口

如果您用浏览器直接打开我们的接口地址，则自动使用我们的浏览器直接访问接口（原标准 JSON 接口），我们会自动向您发送一个 Cookies，作用和 Token 等效。

[https://v2.jinrishici.com/one.json ](https://v2.jinrishici.com/one.json)

此接口  **仅适用于浏览器直接访问**  ，  **不适用于网站调用**  ，应用场景包括：浏览器插件、IOS 捷径访问。如果您贪方便在其他地方直接调用本接口，可能会触发我们的系统判断，导致诗词推荐质量下降。

实际调用本接口时，请务必进行 [接口测试](https://www.jinrishici.com/doc/#test) 确保 Token 每次一致。

### 图片形式调用

![one](https://v2.jinrishici.com/one.svg?font-size=20)

本接口不推荐在自己的网站或 APP 中调用，只有您确实无法添加 JS 或 SDK 时才应该考虑调用。图片调用形式仅限在网站中调用。禁止在其他地方调用。

对于禁用了第三方 Cookies的浏览器（Chrome默认不禁用），本接口可能无法正常跟踪用户导致触发保护机制，降低推荐的效果。请悉知。

图片调用地址为：

```
https://v2.jinrishici.com/one.svg
```

Markdown 格式

```
![今日诗词](https://v2.jinrishici.com/one.svg)
```

HTML 格式

```
<img alt="今日诗词" src="https://v2.jinrishici.com/one.svg">
```

HTML 调用时在所在 DIV 居中并且不会 overflow ：

```
<img alt="今日诗词" src="https://v2.jinrishici.com/one.svg" style="max-width:100%; display: block; margin: 0 auto;">
```

如果您需要自定义图片的文字的大小、间距、颜色，可以在图片地址后面加参数：

| 参数名    | 说明         | 默认值 | 合法范围     |
| --------- | ------------ | ------ | ------------ |
| font-size | 字体大小(px) | 20     | [8,50]       |
| spacing   | 间距(px)     | 1.5    | [0,30]       |
| color     | 颜色         | black  | 颜色英文单词 |

例如：

```
https://v2.jinrishici.com/one.svg?font-size=20&spacing=2&color=blue
```

需要注意的是，颜色目前只接收英文单词， [查看所有颜色英文单词](http://www.w3school.com.cn/cssref/css_colornames.asp)

掘金等一些网站或论坛，会在后端保存图片并替换地址，请注意识别。

他们还出品了 [https://gushi.ci/ ](https://gushi.ci/) ,号称 `调用速度更快` ,好像也没有…