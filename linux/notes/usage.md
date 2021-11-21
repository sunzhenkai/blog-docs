---
title: linux usage
categories: 
	- [linux,notes]
tags:
	- Linux
date: 2020/12/21 9:40:00
update: 2020/12/21 9:40:00
---

# 文件及目录

## 按大小排序打印文件

```shell
$ ls -lSh   # -S: 按大小排序; -h: human readable
$ ls -lShr  # -r: 倒序
$ ls -lShrR # -R: 递归列出子文件夹
```

## 在特定文件内查找内容

**grep**

```shell
$ grep -inr --include pom.xml apollo . # i: 忽略大小写; r: 递归; n: 行号
```

**vim**

```shell
:vimgrep /apollo/g **/pom.xml 
```

## 递归查找特定文件[夹]

```shell
$ find . -name '\.idea'
```

**删除**

```shell
$ find . -name '\.idea' | xargs rm  -r
```

## 目录栈

`dirs` : 查看当前目录栈

- `-v` : 列出目录及其序号
- `-l` : 列出目录全名
- `-c` : 清空目录栈

`pushd` ：改变目录并将原目录压入栈

`popd` : 修改当前目录为栈顶目录并将栈顶目录出栈

```shell
$  ~ dirs
~
$  ~ pushd Downloads 
~/Downloads ~
$  Downloads dirs
~/Downloads ~
$  Downloads popd           
~
$  ~ dirs
~
```

## 递归查看从根至某个路径的权限

```shell
$ namei -om /path/to/check

# 示例
$ namei -om /home/wii/share/
f: /home/wii/share/
 dr-xr-xr-x root root /
 drwxr-xr-x root root home
 drwx------ wii  wii  wii
 drwxrwxrwx wii  wii  share
```

如果一个用户需要访问一个目录，应该有访问其父路径的权限。

# 用户

## 创建用户

```shell
$ useradd -d <home-dir> -s <login-shell> -g <GROUP> username

# 示例
$ useradd -d /home/wii -s /bin/bash -g wheel wii

# 添加到 sudoers 组
$ usermod -aG wheel <user-name>
```

## 免密登录

```shell
# 以配置 主机A 免密登录 主机B 为例
# [A] 生成密钥文件(~/.ssh/id_rsa, ~/.ssh/id_rsa.pub), 如果已生成可略过
$ ssh-keygen -t rsa -C <email>

# [A] 拷贝密钥
$ ssh-copy-id -i ~/.ssh/id_rsa.pub <user@remote-host>

# [B] 修改目录权限
$ chmod 700 ./.ssh 
$ chmod 600 ~/.ssh/authorized_keys

# [A] 登录
$ ssh <remote-host>
```

# 批量杀死进程

```shell
# 按进程名称
$ ps aux | grep <process-name> | awk '{print $2}' | xargs kill -9
# 按端口
$ lsof -i:8200 | awk '{print $2}' | xargs kill -9
```

# 磁盘读写

```shell
$ iotop -o 
```

**参数**

```shell
-o 仅显示有速度的进程
```

# tail 多个远程文件

```shell
# 在一台机器执行
ssh -n user@host1 'tail -f /path/to/file' &
ssh -n user@host2 'tail -f /path/to/file' &
ssh -n user@host3 'tail -f /path/to/file' &
```

# 日期

```shell
# 当前年月日
$ date '+%Y-%m-%d'
2021-11-06
```

