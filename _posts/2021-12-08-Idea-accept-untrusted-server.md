---
layout: post
title: Idea accept untrusted server
date: 2021-12-08 14:02:00 +0800
tags: [miaosha]
comments: false
---
#### 问题描述
> 打开Intellij idea只能accept Untrusted Server Certificate，reject无效。

#### 问题解决
> 参考stackoverflow：https://stackoverflow.com/questions/60092405/untrusted-server-certificate-in-intellij
#### 处理过程
>Preferences -> Tools -> Server Certificates -> Check on "Accept non-trusted certificates automatically"