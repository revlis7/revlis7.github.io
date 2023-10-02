---
layout: post
title: 解决 Win10 可以上网但显示无法访问 Internet 的问题
tags: Win10 无法访问 Internet Surge 网关 旁路由
---

![Win10 No internet connection](/public/images/win10_no_internet_connection.png)

## 解决 Win10 可以上网但显示无法访问 Internet 的问题

利用 Surge tvOS 作为旁路由上网时，可能会遇到 Win10 明明可以访问网络，但是网络连接一直显示无法访问 Internet 的错误。网上有许多教程会解释，说这是因为微软会通过访问域名地址 http://www.msftconnecttest.com/connecttest.txt 或者 http://www.msftncsi.com/ncsi.txt 来确认当前主机网络连接的状态。当这个域名地址不可访问时，就会认为网络连接断开。

这种说法没什么问题，但是不够全面，其实在注册表里还有另一个选项：`ActiveDnsProbeHost`， Win10 会通过解析 `dns.msftncsi.com` 是否为 `131.107.255.255` 来判断网络状态。当你通过 Surge tvOS 作为旁路由访问网络时，由于所有的域名解析都会被转化成 Fake-IP，即 `198.18.*.*` 这样的 IP 地址，所以 Win10 就会认为你无法访问网络。你可以在客户端通过以下命令来判断当前 DNS 解析的结果是否正确：

```bash
➜  ~ nslookup dns.msftncsi.com
Server:		198.18.0.2
Address:	198.18.0.2#53

Non-authoritative answer:
Name:	dns.msftncsi.com
Address: 131.107.255.255
```

解决的办法也很简单，在 Surge tvOS 的配置文件中添加：

```ini
[General]
always-real-ip = dns.msftncsi.com
```

最后的最后，你可能还需要重启一下 Apple TV 来确保配置生效（这可能是当前 Surge tvOS 5.7.0 版本的一个 Bug）
