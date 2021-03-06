---
title: c++ 最佳实践
categories: 
	- [coding, c++]
tags:
	- c++
date: 2022/02/10 00:00:00
update: 2022/02/10 00:00:00
---

# 工程

- 借助 cmake 编写一个库
  - [cmake-cpp-library](https://decovar.dev/blog/2021/03/08/cmake-cpp-library/)

# 工具

- 实现简单的 logger 
  - [nacos cpp client - logger](https://github.com/nacos-group/nacos-sdk-cpp/tree/master/src/log)

# 网络

- 发送请求
  - [借助 curllib 实现](https://curl.se/libcurl/c/libcurl.html)

# 服务治理

## 配置中心

- 实时配置
  - [nacos cpp client -  借助 long polling 机制实现](https://github.com/nacos-group/nacos-sdk-cpp/blob/master/src/listen/ClientWorker.cpp#L333)