---
layout: post
title: 解决 Surge tvOS 在网关模式下无法联网的问题 
tags: Surge tvOS Apple TV 网关
---

![Apple TV 4K](/public/images/apple_tv_4k.png "Apple TV 4K")

## 解决 Surge tvOS 在网关模式下无法联网的问题

Apple TV 最近终于迎来了一次重要的更新：tvOS 17！可以通过安装 Surge、Quantumult X 等软件将 Apple TV 变身为一台旁路由。然而当我按要求配置好 Surge tvOS 后，却发现每过一段时间其他设备就会连不上网络，而 AppleTV 本身却可以正常联网。一开始觉得可能是 AppleTV 进入睡眠以后导致的断网，可是在关闭了AppleTV的睡眠模式后，问题依旧存在。翻了翻网上的讨论，似乎很多人也都遇到了同样的问题。

唯一能确定的是断网以后，其他设备返回的错误都是 DNS 解析失败，所以一定是 DNS 出了问题。但是我翻遍了 Surge 官网也没有找到使用 Surge tvOS 时正确配置客户端 DNS 的方法。于是我还是按 Mac 版 Surge 的增强模式的操作，将客户端的 DNS 指向了 `198.18.0.2` 这个虚拟 IP，在连续使用了几天后，断网的情况终于没有再次发生。所以目前来看，网上许多 Surge tvOS 讨论里说到的将客户段 DNS 指向 AppleTV 本身的 IP 地址的说法，应该是存在问题的，可以尝试使用 `198.18.0.2` 来代替。
