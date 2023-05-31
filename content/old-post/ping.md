---
title: 每日小知识点(二) - 为什么Ping不通外网?
date: '2023-03-21'
tags: ['network', 'daily']
draft: false
summary: Daily Little Knowledge Points
---

# 每日小知识点(二) - 为什么 Ping 不通外网?

## 为什么`ping`不通？

如果使用了代理服务器，但仍无法通过`ping`命令连接到外网(如 Google、Youtube)，可能是以下原因之一：

1. 代理服务器的网络设置不正确：代理服务器可能无法正确地配置或连接到 Internet。当然这个一般不会是主要原因, 但也不排除我们没有配置好相关设置。

2. 代理服务器阻止了`ping`请求：有些代理服务器可能会禁止`ping`请求，以防止攻击或干扰。

3. 防火墙或安全软件阻止了`ping`请求：我们的计算机上的防火墙或安全软件可能会阻止`ping`请求，以保护您的计算机。我们可以尝试暂时关闭防火墙或安全软件，然后再次尝试`ping`请求。

4. **Google 等外网被屏蔽了**: 显然这个对于墙内玩家来说是最主要的原因。

可是我们已经使用了代理服务器，为啥还是会`ping`不通呢？

答：`ping`命令使用 ICMP 协议，这个协议运行在网络层，而且 ICMP 报文需要封装在 IP 数据报里进行传输。因此，`ping`命令需要知道目标 IP 地址，以便构建 IP 数据报发送到网络中。然而，如果目标 IP 地址已被墙或限制，`ping`命令无法到达目标主机。

代理软件（如 V2rayN）提供的代理服务可能并不支持 ICMP 协议。这意味着，如果我们使用的代理服务器不支持 ICMP 协议，则`ping`命令将无法通过代理服务器发送 ICMP 报文到目标主机。因此，我们仍然无法`ping`通目标主机。

## 那如何判断我们可以访问墙外网站呢？

使用命令:

```shell
curl -i google.com
```

"curl -i google.com" 是一个终端命令，用于向网站 "google.com" 发送 HTTP 请求，并在终端中返回响应头。 "-i" 标志告诉 curl 将响应头与响应正文一起包含在输出中。运行此命令时，将看到服务器返回的响应头在终端窗口中打印出来。

`curl -i google.com` 和 `ping google.com`的区别：
`curl -i` 命令可以使用代理服务器进行 HTTP 请求，只需要在命令中指定代理服务器的地址和端口号即可。而`ping` 命令默认不使用代理服务器。