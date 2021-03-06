---
title: consul usage
categories: 
	- [架构,注册发现,consul]
tags:
	- consul
date: 2021/12/08 00:00:00
update: 2021/12/08 00:00:00
---

# 启动

```shell
$ consul agent -dev -bind=0.0.0.0 -client=0.0.0.0 -advertise=127.0.0.1
```

# 高可用

- [nginx+consul](https://chabik.com/2019/12/dynamic-upstreams-in-nginx-w-consul/)

# 接口

## 查询所有服务

```shell
curl -XGET http://localhost:8500/v1/catalog/services
```

## 查询服务所有监控实例

```shell
curl -XGET http://localhost:8500/v1/health/service/:servicename
```

## 列出所有节点

```shell
curl -XGET http://localhost:8500/v1/catalog/nodes
```

## 强制去除节点

```shell
curl -XPUT http://localhost:8500/v1/agent/force-leave/:node_name	
```

# KV

## 导入导出

[export](https://www.consul.io/commands/kv/export)，[import](https://www.consul.io/commands/kv/import#stale)。

```shell
consul kv export > data.json         # 导出所有
consul kv export online/ > data.json # 导出 online 前缀
```

```shell
consul kv import @data.json         # 文件导入, 需要在文件名前加 @
cat data.json | consul kv import -  # 通过管道导入
```

## 查询

```shell
# 列出所有 key
curl --location --request GET 'http://127.0.0.1:8500/v1/kv/?keys'
```

