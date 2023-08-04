---
layout: post
title: 在 Linux 下使用 L2TP VPN
tags: Linux L2TP VPN
---

如果你在 Linux 下使用 L2TP VPN 时遇到无法连接的问题，你或许可以从以下几点来定位问题

* journalctl -u NetworkManager.service
* sudo /usr/libexec/nm-l2tp-service --debug
* sudo sed -e '/blacklist l2tp_netlink/s/^b/#b/g' -i /etc/modprobe.d/l2tp_netlink-blacklist.conf
* sudo sed -e '/blacklist l2tp_ppp/s/^b/#b/g' -i /etc/modprobe.d/l2tp_ppp-blacklist.conf
* ip forwarding
* ipv4_forward
* iptables FORWARD POSTROUTING

TBD
