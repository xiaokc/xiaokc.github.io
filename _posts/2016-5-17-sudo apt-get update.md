---
layout: post
title: sudo apt-get update失败的解决方法总结
published: true
---
***这里针对“Fail fetch ... error”***
1.首先想到是软件源不对，导致update无法获取，先更新软件源列表

`sudo cp /etc/apt/sources.list  /etc/apt/sources.list.backup`

将sources.list中的内容替换为网上可用的软件源，之后在终端再执行`sudo apt-get update`命令

2.如果1失败，有可能是nameserver不全，域名服务器无法解析ip，更新resolv.conf文件：

`sudo vim /etc/resolvconf/resolv.conf.d/base`

添加以下两行（google的DNS）

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

之后保存并退出（:wq）文件后重启服务：

`sudo /etc/init.d/resolveconf restart`

3.如果2失败，终端不能上网，去检查浏览器是否通过代理才能上网的,如果是，则终端也需要配置同样的代理

> （http://askubuntu.com/questions/308809/no-internet-for-terminal-connect-through-a-proxy）


`cd /etc/apt`

创建一个新文件，名称任意，这里叫做proxies:

`sudo vim proxies`

添加这两行：（与浏览器的代理设置相同）

```
Acquire::http::Proxy “http://proxy_url:proxy_port/”;
Acquire::ftp::Proxy “http://proxy_url:proxy_port/”;
```
4.如果3失败，（好惨啊），我还没碰到，继续google，继续百度，加油

