---
title: '拿 OneDrive 做共享云，方便速度还贼快'
date: 2020-10-23 15:22:10
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
![](https://oss.qust.me/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-23%20231252.png)
此前有看到过拿 OneDrive 做共享云的，速度很快，也不走自己服务器流量。最近开了 Office 365 车，正好想到此事。看了几个 OneDrive 共享的程序，感觉配置有点复杂，为了方便自己折腾也或许能给别人提供便利就打包了个 Caddy 2 和 OneList go 版本的 Docker。<!--more-->

**cloud.qust.me 可以看看我的共享 OneDrive，分享文件下载十分方便。** 

![](https://oss.qust.me/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-23%20231252.png)

## 准备

1. 一台 vps 服务器(会占用 443 和 80 端口)
2. 已经解析好了到该服务器的域名
3. OneDrive 账户

## 安装

### 安装好 Docker 

```
 curl -fsSL https://get.docker.com -o get-docker.sh  && \
 bash get-docker.sh
```

### 获取授权

根据你的账户情况选择

#### [国际版, 个人版(家庭版)](https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=78d4dc35-7e46-42c6-9023-2d39314433a5&response_type=code&redirect_uri=http://localhost/onedrive-login&response_mode=query&scope=offline_access%20User.Read%20Files.ReadWrite.All)

#### [中国版(世纪互联)](https://login.chinacloudapi.cn/common/oauth2/v2.0/authorize?client_id=dfe36e60-6133-48cf-869f-4d15b8354769&response_type=code&redirect_uri=http://localhost/onedrive-login&response_mode=query&scope=offline_access%20User.Read%20Files.ReadWrite.All)

点击上述链接后浏览器会跳转到 http://localhost/onedrive-login?code=XXXX 这样的，复制下面会用到。

### 运行

授权链接：复制上面的跳转

类型选择：

* 国际版 填 a
* 家庭版个人版填 ms
* 世纪互联版填  cn

域名：此 VPS 绑定的域名，Caddy 获取 SSL 用

子目录：根目录文件名，比如共享 OneDrive 根路径下面的 share 文件夹，填 share 即可；不填则表示共享根目录。

```
docker run -d --rm --name onelist -p 443:443 -p 80:80 pengchujin/onelist:0.14 授权链接 类型选择 域名 子目录 && sleep 3s && docker logs onelist
```

像我 填好就是这样：

```
docker run -d --rm --name onelist -p 443:443 -p 80:80 pengchujin/onelist:0.14 http://localhost/onedrive-login?code=M.R3_BL2.a41510da-4b4a-d332-1ba2-xxxxxxxxxx a cloud.qust.me share && sleep 3s && docker logs onelist
```

运行完浏览器打开 你的域名 应该即可共享。

## 可能会遇到的问题

查看日志：

```
docker logs onelist 
```

如果没有日志，很有可能是授权链接错误。

停止共享：

```
docker stop onelist
```

1. 授权的链接用一次就会失效，请每次单独生成。
2. 如果打开域名，显示 No Found，应该是无该目录或者该目录下无文件（如果是 OneDrive 刚添加的同步任然需要一段时间）

**欢迎提出问题。**

**感谢**：[MoeClub](https://github.com/MoeClub) 的 [OneList](https://github.com/MoeClub/OneList/tree/master/Rewrite) ，以及 Caddy 2。