---
title: '斐讯n1配置旁路由后无法访问网络'
date: 2020-05-23 03:00:26
tags: []
published: true
hideInList: false
feature: 
isTop: false
---

![](https://oss.qust.me/img/20200523120019.jpg)

斐讯 n1 做旁路由，碰见部分路由器做主路由例如：小米、华为、linksys 等经常会碰见配置好旁路由设置无法上网，或者国内网络无法打开，或国内网络很慢。<!--more-->

参考了恩山 这个帖子 [N1盒子] [【终极指南】关于N1做旁路由添加 iptables 自定义防火墙规则的见解](https://www.right.com.cn/FORUM/thread-2983767-1-1.html)

### 方法一

* 选择 **网络** — **防火墙** — **自定义防火墙**  末尾添加上这段

![](https://oss.qust.me/img/20200523120019.jpg)
  
```
iptables -t nat -I POSTROUTING -o eth0 -j MASQUERADE
```

解释：用来 “iptables 修改 NAT 表，使经过 eth0 的网卡的流量的源 IP 伪装成 eth0 的 IP，而且是动态伪装（直接读取 eth0 的 IP 地址）”

### 方法二

我个人因为试过的路由器比较多，方法一碰见很多路由器其实没啥作用。这里添加wan 口就可以。

* 第一步：打开 **网络**—**接口**—**lan 修改**—**物理设置**

  ![](https://oss.qust.me/img/20200523120418.jpg)

  取消勾选桥接接口，下面选择 “以太网适配器: "eth0()"”  保存应用

* 第二步 打开 **网络**—**接口**—**添加新接口**

  ![](https://oss.qust.me/img/20200523120742.jpg)

  新的接口名称：wan

  新接口的协议：DHCP客户端

  包含以下接口选择：“以太网适配器: "eth0()"” 

  然后点提交

这时候应该都解决问题，能打开网站了。

 