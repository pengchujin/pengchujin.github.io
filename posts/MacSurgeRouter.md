---
title: 'Surge 把你的 Mac 变成最强路由器'
date: 2021-01-16 15:59:01
tags: []
published: true
hideInList: false
feature: 
isTop: false
---

最近一两年我用过很多路由器：斐讯 n1、NanoPi r2s、NanoPi r4s、华硕 ax86u 等等都是蛮热门的产品。但在我前俩天买了用了 Mac 的 Surge 当作家里的路由器后，方便和体验真的是回不去了。  

关于 surge 4 的教程特别是 DHCP 当做路由器，我看网上的资料教程实在是很少，自己查也废了不少功夫，就写个教程做个视频分享给大家。温馨提示：**首先你得有台放在家里，最好接着网线的 Mac 系统电脑；还有就是你要花几百块买 Surge 这个软件。**

Surge 是一个很强大的网络工具，不仅仅是一个代理软件；目前 Surge 是版本买断制度的，你可以直接在[官网购买](https://nssurge.com/buy_now)，然后就能一直使用 Surge 4 这个大的版本了。<!--more-->

## Surge DHCP 接管网络

###  1 添加 Surge 的配置文件

你订阅的服务应该会给 Surge 的**订阅链接**，如果没有也没关系，你可以通过第三方 [订阅转换](https://bianyuan.xyz) 生成（推荐用这个，分流会丰富合理很多）：

![](https://oss.qust.me/img/20210116211324.png)

1. 订阅链接填上你的 v2ray、ss 、trojan 的订阅
2. 客户端选择 surge 4
3. 选择生成订阅链接就好了

打开 surge 设置中的**配置**

![](https://oss.qust.me/img/20210116211500.png)

选择从 url 安装配置

![](https://oss.qust.me/img/20210116211555.png)

粘贴上你的配置文件订阅地址后选择完成

![](https://oss.qust.me/img/20210116211622.png)

选中刚才添加的点击 **应用**

![](https://oss.qust.me/img/20210116211641.png)

在策略里选择 **规则判定**，这时候你应该就能愉快的上网了。

![](https://oss.qust.me/img/20210116211714.png)

如果不行可以重新退出打开下 surge，并检查是否打开了 **设置为系统代理** 和 **增强模式**。

![](https://oss.qust.me/img/20210116211730.png)

### 2 配置 Surge DHCP 接管网络

#### 设置电脑 IP 为静态IP

打开 **系统偏好设置-网络**，选择以太网（也就是网线接口），配置 IPv4 选择 **使用 DHCP（手动设定地址）**，我的路由器是 192.168.88.1 所以 IP 地址我就填 192.168.88.2，只用修改最后一位在 2-225 之间就行。（如果你的路由器是 192.168.31.1 你的 IP 地址就可以填 192.168.31.2，以此类推）随后选择 **应用**。

![](https://oss.qust.me/img/20210116212721.png)

#### 关闭路由器 DHCP

一般都在 **内部网络-DHCP服务器** 选项里，关闭启用 DHCP， 保存并应用。（各家系统的设置位置可能有差别，但基本都是有 DHCP 开关选项的）

![](https://oss.qust.me/img/20210116212428.png)

#### 打开 Surge DHCP 选项

在左侧 **设备** 里，点开后有 **DHCP 服务器** 开关，点开后请认真看下内容，然后选择下一步。

![](https://oss.qust.me/img/20210116221722.png)

网络设备和你上面设置固定的 IP 的一致，插网线的选择 **Ethernet** 就行，继续下一步。

![](https://oss.qust.me/img/20210116212820.png)

Surge 会检测当前网络环境是否有 DHCP 设置，如果上面你正确关闭了 路由器 DHCP 这里应该能直接过去。

![](https://oss.qust.me/img/20210116213020.png)

选择 Surge 默认的设置点击**完成**即可，如果你懂的可以自行修改。

![](https://oss.qust.me/img/20210116213337.png)

把你其它设备**重新连接 wifi 或者关闭路由器 wifi 再打开**即可看到 设备里新增设备。

![](https://oss.qust.me/img/20210116213153.png)

如果你想你连接的设备通过 Surge 走代理服务，你可以右键选择设备名然后选择 **使用 Surge 作为网关**，再**设备重新连接或者关闭路由器 wifi 再打开**即可。

![](https://oss.qust.me/img/20210116213225.png)

## Surge DHCP 使用模块

我只购买了 Mac 版的 Surge，但我想我的手机也能实现除了能用代理外，也能使用 微博去广告、Netflix 有评分、看 tiktok 不用拔掉 sim 卡。如果你也想使用 Module 的功能可以继续往下看，这部分可能稍微有点麻烦。

#### Mac 创建证书

1. 打开 **钥匙串访问 app**（Keychain Access.app）  

2. 选择菜单项 钥匙串访问 （Keychain Access） -> 证书助理 （Certificate Assistant） -> 创建证书颁发机构 Create Certificate Authority…

   ![](https://oss.qust.me/img/20210116221318.png)

3. 证书参数（名字邮箱随意填写）点击创建即可，记下倒出的位置，后面要用到。

   ![](https://oss.qust.me/img/20210116222932.png)

4. 证书创建后，在左侧选择 **我的证书** （My Certificates），然后在右侧列表中找到该证书，右键点击证书，选择导出，**导出格式选择为 .p12 格式，导出时需要设置 密码 （passphrase），不可设置为空。若不可选择 p12 格式，请确认先切换到我的证书 （My Certificates） 后再进行导出。**

   ![](https://oss.qust.me/img/20210116223054.png)

   ![](https://oss.qust.me/img/20210116223108.png)

5. 将证书复制到左侧 Keychains 列表中的 System 中 粘贴 （不做该步骤会使得 Safari 不认该 CA，不过 Chrome 可以正常工作）输入刚才添加的密码完成。

   ![](https://oss.qust.me/img/20210116223550.png)

   ![](https://oss.qust.me/img/20210116223604.png)

6. 双击证书，将该证书标记为可信，关闭窗口输入登录密码确认操作。

   ![](https://oss.qust.me/img/20210116223630.png)

7. 将得到的 Certificates.p12 文件用在 terminal 中进行 base64 编码，得到结果会用到。

   ```
   base64 SurgeModule.p12 
   ```

   ![](https://oss.qust.me/img/20210116224319.png)

8. 编辑 Surge 的配置文件（设置-配置-在 Finder 中找到配置；然后用文本编辑器打开），加入 MITM 段。ca-passphrase = 填写你之前的密码，ca-p12 = 填写你刚 base64 出来的结果。

   ```
   [MITM]
   enable = true
   tcp-connection = true
   hostname = *facebook.com, *pinboard.in
   ca-passphrase = 123456
   ca-p12 = MIIJtQIBAzCCCXwGCSqGSIb3DQ…..
   ```

   ![](https://oss.qust.me/img/20210116224523.png)

   ![](https://oss.qust.me/img/20210116224533.png)

9. 打开再文件里右键刚才编辑好的文件选 Surge 打开，选择覆盖，便会使用新的配置文件。

   ![](https://oss.qust.me/img/20210116224637.png)

   ![](https://oss.qust.me/img/20210116224646.png)

10. 在 **解密** 中打开 HTTPS 解密开关。

    ![](https://oss.qust.me/img/20210116224919.png)

#### 发送证书到手机安装

1. 在 Surge **解密** 中选择为 iOS 模拟器倒出证书

   ![](https://oss.qust.me/img/20210116225450.png)

2. 发送证书到手机（airdrop 或者别的方式发到手机上）。

   ![](https://oss.qust.me/img/20210116231352.png)

3. 在手机打开描述文件，设置里选择已下载的描述文件-安装描述文件-选择同意输入密码即可。

   ![](https://oss.qust.me/img/20210116225607.PNG)

   ![](https://oss.qust.me/img/20210116231010.PNG)

   ![](https://oss.qust.me/img/20210116231016.PNG)

4. 最后在 **设置**-**通用**-**关于手机** 打开对证书的信任。

   ![](https://oss.qust.me/img/20210116231307.PNG)

#### Surge 安装打开模块

在**设置**中打开**模块**选择**从 URL 安装模块**，安装这个模块选择开启后应用即可。

https://raw.githubusercontent.com/pengchujin/SurgeMacModule/main/modules.sgmodule

![](https://oss.qust.me/img/20210116232936.png)

![](https://oss.qust.me/img/20210116234315.png)

更多模块功能可以看看这里（上面是我做了一个合并的，免拔卡看 tiktok、Netflix 评分、微博去广告 等等）

* https://github.com/lhie1/Rules/tree/master/Surge/Surge%203/Module
* https://github.com/Tartarus2014/Surge-Script
* https://github.com/nzw9314/Surge/tree/master/Module

也可以看看这个 module 使用教程：https://merlinblog.xyz/wiki/surge-module.html

## 总结

如果有有问题可以看看 surge 开发者详细的文章：https://blankwonder.medium.com

surge 官方功能手册：https://manual.nssurge.com/book/understanding-surge/cn/

如果对这篇教程有疑问也可以发邮件给我 pengchujin@hotmail.com

