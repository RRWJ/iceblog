---
layout: post
title: Goland and Configure error
subtitle: gopath
date: 2022-05-05 14:36:00 +0800
tags: [Go]
comments: false
---
### 配置GoRoot
在Go官网下载后，Linux下默认路径为：
```
$ /usr/local/go/
```
主要包括go相关的编译器和工具 compilers/tools
### 配置 GoPath
GoPath路径中包含自定义的go项目以及第三方库，支持自定义路径。
>
1. 配置好gopath后，命令行输入go env 得到的路径与echo $GOROOT得到的路径不符合
参考链接 https://stackoverflow.com/questions/54372880/although-gopath-is-set-echo-gopath-returns-nothing
2. github讨论问题 https://github.com/golang/go/issues/38896
3. goland配置goroot and gopath https://www.jetbrains.com/help/go/configuring-goroot-and-gopath.html
### go语言开发文档
.go程序运行时，需要将编程语言编译为.mod进而在机器上运行
https://go.dev/doc/code