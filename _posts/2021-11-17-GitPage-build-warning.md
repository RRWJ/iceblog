---
layout: post
title:  Page build warning
tags: [Github]
comments: true
---

#### 每次push都发送一封邮件，强迫症很蓝瘦;(
```
The page build completed successfully, but returned the following warning for the `main` branch:

The custom domain `#填上自己的域名（如果有申请）` is not properly formatted. See https://docs.github.com/articles/troubleshooting-custom-domains/#github-repository-setup-errors for more information.

For information on troubleshooting Jekyll see:

  https://docs.github.com/articles/troubleshooting-jekyll-builds
```
```
Warning: We strongly recommend not using wildcard DNS records, such as *.example.com. A wildcard DNS record will allow anyone to host a GitHub Pages site at one of your subdomains.
```
#### 参考List：
#### 1. GitPage原文档配置个人域名
##### https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages
#### 2. StackOverflow问答
##### https://stackoverflow.com/questions/9082499/custom-domain-for-github-project-pages

####  配置过程：
#### 1. 购买域名18元/年；
#### 2. 查看Github Pages在国外的IP地址；
```
ping xxx.github.io
```
#### 3. 修改DNS，参考链接：
#### https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages