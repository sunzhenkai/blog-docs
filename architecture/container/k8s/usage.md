---
title: k8s usage
categories: 
	- [架构,container,k8s]
tags:
	- k8s
date: 2022/06/09 00:00:00
update: 2022/06/09 00:00:00
---

# 节点管理

## 删除节点

```shell
$ sudo kubeadm reset cleanup-node  # master 节点也可以清除
```

# Pod 管理

```shell
# 查看 pod  信息
$ kubectl get pods -A  # A = all-namespaces

# 删除 pod
$ kubectl delete pod <name> --namespace=<ns>

# 查看 pod 详情; ip 等
$ kubectl describe pod <name> --namespace=<ns>
```