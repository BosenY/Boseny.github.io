---
title: 关于切换到https
date: 2018-02-07 09:01:01
tags:
- 日常
---

## 起因

其实不切https也没什么性能上的问题，就是想把chrome上的安全绿锁头显示出来；从另一方面讲，还能减少一些http劫持(这个其实深层次的我也没研究过，包括DNS劫持之类的...)和运营商劫持，切到https后，看上去好像是减少了一些被劫持的几率。
<!--more-->
## 具体操作

因为是静态资源，也不想买国内的服务器(有国外的vps了)，所以就用github page，至于简单的如何配置hexo blog这里就不陈述了，反正百度一大把。

因为github page不能上传ssl证书，所以就用CDN实现反向代理，原理基本上就是利用CDN服务器反向代理到github page 因为CDN服务器是提供https服务的，所以最终自己的域名也会变成https。

这里我用的是<a href="https://www.cloudflare.com/">CloudFlare</a>：
![](http://owgraa3f3.bkt.clouddn.com/18-2-7/72109306.jpg)

- 注册一个账号并登陆
- 添加一个站点把自定义的域名配入,等扫描，扫描结束点击继续
- DNS项配入，把自己的域名和github page的ip地址配入到DNS解析当中，具体就是创建一个CNAME类型，这里填写的是你原来github page的域名， 然后再创建两个类型是A，name是自己的域名，值是github的ip 192.30.252.153和192.30.252.154，类似于底下这张图：
![](http://owgraa3f3.bkt.clouddn.com/18-2-7/42228843.jpg)
- 然后把下面的DNS服务器里的地址复制好，将自己购买的域名的服务器下的DNS改成这个
- 让在Crypto选项处设置ssl为flexible
- 在page rules中设置路由规则。然后设置两条规则<em style="color: red;">Always use https</em>一条url是`http://域名/` ，另一条是`http://域名/*`，这样就能开启强制https
- 都配置好在12小时以内就会生效，然后博客就正式切到https了