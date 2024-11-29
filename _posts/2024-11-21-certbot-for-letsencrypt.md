---
layout: post
date: 2024-11-21
author: Leo
permalink: /certbot-for-letsencrypt-20241121/

title: "使用 certbot 申请免费 SSL 证书"
category: "programme"
tags: [https, certbot, letsencrypt]
---


现在网站使用 https 已经成为标配，但是 SSL 证书最便宜的 DV 证书也要几百块钱一年，对于个人开发者来说很不划算。好在，我们有[Let's Encrypt](https://letsencrypt.org/)，它是能提供免费的 SSL 证书，应该也是市面上使用最广泛的免费 DV 证书了。

# 原理
一点开[Let's Encrypt](https://letsencrypt.org/)还是有点懵的，按照在其他平台申请 SSL 证书的逻辑，它尽然不用注册，那怎么管理证书呢？随着不断的了解，对它也越来越佩服。

[Let's Encrypt](https://letsencrypt.org/)贡献两个主要的东西
- [ACME protocol](https://datatracker.ietf.org/doc/html/rfc8555)
- [boulder](https://github.com/letsencrypt/boulder)

ACME 全称 Automatic Certificate Management Environment。它提供一套自动证书管理的规范，这套规范中包含客户端与服务端。而[boulder](https://github.com/letsencrypt/boulder)就是[Let's Encrypt](https://letsencrypt.org/)提供的一套开源的证书颁发软件。ACME 客户端官方没提供，只要支持 ACME 协议都可以实现。目前，官方推荐的客户端是[certbot](https://certbot.eff.org/)。

证书颁发机构只需要确认你拥有该域名的所有权，就可以帮你生成证书（需要注意[Let's Encrypt](https://letsencrypt.org/)并不支持 OV 和 EV 证书）。

在服务器上运行 ACME 客户端，已自动化的方法确认用户对于域名的所有权，然后向[Let's Encrypt](https://letsencrypt.org/)服务端申请证书，通过后，既可以得到所需要的 SSL 证书。

[Let's Encrypt](https://letsencrypt.org/)生成的免费证书有效期为 90 天，但是它也支持自动续签。


# 使用
以下操作，基于 CentOS7.8 + Nginx 服务器。

## 安装 certbot
它是一款在 Linux 上使用的现代包管理工具。

```shell
# Centos7 中安装 snapd
sudo yum install epel-release
sudo yum install snapd
sudo systemctl enable --now snapd.socket
sudo ln -s /var/lib/snapd/snap /snap

# 查看 snapd 服务状态
sudo systemctl status snapd

# 安装 certbot
snap install --classic certbot
```

可以参考官方文档：https://certbot.eff.org/instructions?ws=nginx&os=snap

## 申请证书
certbot 有一些傻瓜式的方式可以直接一键生成证书并安装。但是这并不是我需要的，我只希望他帮我生成证书，然后自己在 Nginx 中配置。

```shell
sudo certbot certonly --webroot -w /path/to/webroot -d example.com -d www.example.com
```

这条指令的作用是以 http 的方式验证域名并单独生成证书。`-w`指定域名所在的根目录，`-d`指定需要验证的域名。以上命令成功后，它会在`/etc/letsencrypt/live/example.com/`目录中生成证书。

## 部署证书
部署证书的操作，另行搜索即可。

## 自动续签
在证书还有 30 天过期时，重新验证域名的所有权。验证成功重新颁发证书，并重启 Nginx 服务。
[certbot](https://certbot.eff.org/)已经将这些功能实现，只需要进行少量配置即可。
```shell
# 验证是否能够续签
sudo certbot renew --dry-run

# crontab 中添加定时调度
sudo crontab -e
0 3 * * * certbot renew --quiet --deploy-hook "nginx -s reload"

```
验证续签功能通过，说明当前环境没问题。就可以将续签的指令添加到 crontab 中每天晚上 3 点检测一次。`--deploy-hook`指定续签成功后 reload 配置。

## 其他
```shell
# 强制更新证书
sudo certbot certonly --webroot -w /path/to/webroot --force-renewal --deploy-hook "nginx -s reload" -d example.com -d www.example.com
```


# 引用
- [https://letsencrypt.org/](https://letsencrypt.org/)
- [https://datatracker.ietf.org/doc/html/rfc8555](https://datatracker.ietf.org/doc/html/rfc8555)
- [https://github.com/letsencrypt/boulder](https://github.com/letsencrypt/boulder)
- [https://certbot.eff.org/](https://certbot.eff.org/)