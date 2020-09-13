---
layout: post
title: 'Codeforces 镜像站搭建'
subtitle: 'Codeforces 高速访问'
date: 2020-08-21
categories: 发现
cover: 'https://s1.ax1x.com/2020/08/25/dc05eU.png'
tags: Codeforces
---

# Codeforces 镜像站搭建

```
　　Codeforces十分慢是怎么回事呢？Codeforces相信大家都很熟悉，但是Codeforces十分慢是怎么回事呢，下面就让小编带大家一起了解吧。
　　Codeforces十分慢，其实就是出口带宽不够，大家可能会很惊讶Codeforces怎么会十分慢呢？但事实就是这样，小编也感到非常惊讶。
　　这就是关于Codeforces十分慢的事情了，大家有什么想法呢，欢迎在评论区告诉小编一起讨论哦！
```

# 为什么 Codeforces 十分慢?

各家运营商人均用户出口带宽量比较如下：

```
中国联通 ＞ 中国电信 ＞ 中国移动
```

所以如果用的是联通网络，那么上 Codeforces 和上百度基本没啥区别。



电信情况比较特殊：

> - 中国电信目前拥有两条线路，一条是 163 骨干网（ChinaNet），另一条就是 CN2 网络；
> - 相对 CN2 而言，有的人又习惯称 163 骨干网为 CN1，163 网是中国电信建设的最早的一个网络，它为超过 1 亿的中国电信用户承载包括连往境外的，普通质量的互联网业务。身为电信用户，如果在晚上连接境外网络总是感觉卡顿，丢包高，99.99%的原因都是因为走的这张网，大家一起挤，线路就 boom 了；
> - CN2，即“ChinaNet Next Carrying Network（ChinaNet 的下一代承载网络）”，在 2005 年投入使用，最初架设的目标，是提供一个拓扑合理，架构先进，建设科学，用于满足未来 10-20 年替代 163 网成为未来新骨干网的网络（这个 flag 还未实现），CN2 网络能够同时承载语音、数据、视频、全球互联等业务，尤其是全球互联方面，相对于 163 网而言，CN2 网络的低丢包、低延时、轻负载，让众多用户趋之若鹜；
> - 据统计，在中国电信的总网络连接中，163 网络承担了 85% 的网络流量，其余的 15% 流量，由 CN2 网络承担；

并且在[V2EX](https://www.v2ex.com/)上，有用户发现中国电信还会对未开通`氮气瓶/电信精品网`的用户进行随机丢包，那么....

据其他用户称， CN2 线路也差不多满负荷了，但还是比163骨干网要好点。

但是丢包和延迟对网速影响也很严重：    

![](https://s1.ax1x.com/2020/08/21/dNPcZj.png)

下面这张图是在移动网络下午5点左右 Ping 的，可以看到了丢包达到了75%，延迟也有277ms。

![](https://s1.ax1x.com/2020/08/21/dNpjW8.png)

去 <https://ipip.net> 查下这个IP的物理位置：

![](https://s1.ax1x.com/2020/08/21/dNi61K.png)

发现在俄罗斯莫斯科。



# 怎么解决？

那么搞个镜像站呗。

十分有名的 Codeforce s镜像站<https://codeforces.ml/>，去查IP，是 Cloudflare 的。

Cloudflare 的 CDN 遍及100个国家/地区的200个城市，最近的节点在香港。（国内的是百度云加速的节点）

香港不用跨洋电缆，直接就可以连接上，当然快喽。



最常用的镜像站搭建方法就是nginx反向代理了。



比较喜欢用[宝塔](https://bt.cn)来搞服务器，主要是给你了一个GUI……



其实搞反向代理很简单，把nginx装好之后，更改nginx.conf：

```
server {
		#反向代理完之后访问的端口,http填80,https填443
        listen       80;
        #反向代理完之后访问的域名,没域名可以填服务器ip
        server_name  test.com;
		location / {
			#要代理的地址,http/https不能漏
            proxy_pass http://321.com;
            #原服务器的index地址,按照先后顺序访问
            index  index.html index.htm index.jsp;
        }
}
```

再重启nginx，代理就搞定了。

如果要代理的网站强制使用https，那么该服务器也需要配置https。



宝塔面板里还有个`开启缓存`的选项，如果开了，最好只自用，不然可能我登录了我的账号缓存过之后，你再访问就变成缓存内容了。

不过：搭 Codeforces 镜像站最好还是在香港服务器上搭，这样访问会快很多。

# 写在最后

![dNZAYj.png](https://s1.ax1x.com/2020/08/21/dNZAYj.png)

所以现在<https://codeforces.ml/>也在登录页面提示：

```
比赛开始时巨大的访问量，可能导致镜像站被误封，一般来说 5 到 10 分钟之后会恢复正常。
为了避免浪费宝贵的时间，建议您在比赛时使用 m1.codeforces.ml、m2.codeforces.ml、m3.codeforces.ml，需要看榜或者叉人时再使用主站。
```



其实家里有两条宽带也是很舒服的，家里有一条移动宽带，一条华数宽带（走的是联通国际出口，有公网IP，上下行对等），打 Codeforces 时也是很快的。

写文章不易，求点赞qwq

# 参考资料

<https://zhuanlan.zhihu.com/p/64467370>

<https://www.cnblogs.com/ysocean/p/9392908.html>



本文采用[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)许可证进行许可。
