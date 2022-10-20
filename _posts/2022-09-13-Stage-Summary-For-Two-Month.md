---
layout: post
title: Stage Summary For Two Month
date: 2022-09-13
tags: [Spring]
comments: false
---

### 一、Workflow 项目开发
> 入职至今参与两个Etcd集群相关的开发项目，脱离不开Spring MVC三件套: controller->service->dao，收获：从底层数据库到顶层前端完成了两个微服务之间的通信，可改进的点：controller层添加拦截器和路由器可以分发功能；
### 二、MicroService
>1.目前两个微服务通过http连接，后续采用rpc;
>2.curl命令发送请求； curl -X [Post|Get] -H [Header] -d[RequestBody]

### 三、Kubernetes
> 在第二个微服务中需要client-java接口访问k8s资源，通过laberSeletor对cluserName筛选。
参考链接：
1. 根据clusterName查询所有pod信息，并返回List<V1Pod>
 V1PodList list = api.listPodForAllNamespaces(null, null, null, "clusterName="+cluster, null, null, null, null, null);
 return list.getItems();
2. 常用的kubectl命令：https://cloud.tencent.com/developer/article/1769990