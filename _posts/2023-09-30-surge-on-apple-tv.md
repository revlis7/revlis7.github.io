---
layout: post
title: 解决 Surge tvOS 在网关模式下无法联网的问题 
tags: Surge tvOS Apple TV 网关
---

![Apple TV 4K](/public/images/apple_tv_4k.png "Apple TV 4K")

## 解决 Surge tvOS 在网关模式下无法联网的问题

Apple TV 最近终于迎来了一次重要的更新：tvOS 17！可以通过安装 Surge、Quantumult X 等软件将 Apple TV 变身为一台旁路由。可是我按要求配置好 Surge tvOS 后，却发现每过一段时间其他设备就会连不上网络，而AppleTV本身却可以正常联网。一开始我觉得可能是AppleTV进入睡眠以后导致的断网，可是我在关闭了AppleTV的睡眠模式后，问题依旧存在。翻了翻网上的讨论，似乎很多人也都遇到了同样的问题。

唯一能确定的是断网以后，其他设备返回的错误都是DNS解析失败，所以一定是DNS出了问题。但是我翻遍了官网也没有找到使用Surge tvOS时正确配置客户端DNS的方法。于是我还是按Mac版Surge的增强模式的操作，将客户端的DNS指向了 `198.18.0.2` 这个虚拟IP，在连续使用了几天后，断网的情况终于没有再次发生。所以目前来看，网上许多Surge tvOS讨论里说到的将客户段DNS指向AppleTV本身的IP地址的说法，应该是存在问题的。
