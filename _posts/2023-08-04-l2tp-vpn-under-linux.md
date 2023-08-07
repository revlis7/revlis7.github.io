---
layout: post
title: 排查在 Linux 下使用 L2TP VPN 无法连接的问题
tags: Linux Fedora L2TP VPN
---

### 检查 NetworkManager 日志

如果你在 Linux 下使用 L2TP VPN 时遇到无法连接的问题，提示：

```
Activation of network connection failed
```

可以通过检查 NetworkManager 日志来尝试定位问题，以 Fedora 38 为例，查看日志：

```bash
journalctl -u NetworkManager.service
```

如下列日志中提示，内核中没有打开 L2TP 的支持：

```
Aug 06 01:09:09 fedora38 NetworkManager[5932]: xl2tpd[5932]: Not looking for kernel SAref support.
Aug 06 01:09:09 fedora38 NetworkManager[5932]: xl2tpd[5932]: L2TP kernel support not detected (try modprobing l2tp_ppp and pppol2tp)
```

### 打开 L2TP 内核模块支持

注释掉 `/etc/modprobe.d/l2tp_netlink-blacklist.conf` 和 `/etc/modprobe.d/l2tp_ppp-blacklist.conf` 两个文件中的 `blacklist` 行，或使用命令：

```bash
sudo sed -e '/blacklist l2tp_netlink/s/^b/#b/g' -i /etc/modprobe.d/l2tp_netlink-blacklist.conf
sudo sed -e '/blacklist l2tp_ppp/s/^b/#b/g' -i /etc/modprobe.d/l2tp_ppp-blacklist.conf
```

打开内核模块支持并重启即可。这里 L2TP 内核模块之所以默认被列入黑名单是 Linux 为了提升系统安全性，以及防止未来可能出现的安全漏洞而做的选择。

### 更多的错误信息

如果 `journalctl` 命令提供的错误信息还不够详细，可以使用以下命令并尝试连接 VPN：

```bash
sudo /usr/libexec/nm-l2tp-service --debug
```

根据错误提示来修改对应的配置，比如你在 VPN 配置中使用了不支持的加密算法时，就可以在这里看到，只要将对应的算法从列表中删除即可。
