---
name: cursor-server-remote-install
description: 指导在无法直连 Cursor 服务器的远端 Ubuntu 主机上，通过离线流程安装或升级 Cursor Server。在远端 Ubuntu 上进行 Cursor Server 的安装/升级、或用户提及离线安装/无法访问 Cursor 服务器时使用。
---

# Cursor Server 远端主机离线安装与升级

当远端 Ubuntu 主机**无法直接访问 Cursor 相关服务器**时，必须采用离线流程，不得在远端直接执行会访问官网/CDN 的安装或升级命令。

## 正确流程

1. **在可联网主机上下载**
   - 在能访问 Cursor 的机器上，下载对应平台（linux-x64）的 Cursor Server 安装/升级包（如 `.tar.gz`）。
   - 下载地址以 Cursor 官方文档/发布页为准。

2. **传输到远端 Ubuntu**
   - 使用 `scp`、`rsync`、SFTP 或项目约定方式，将安装/升级包从工作主机传到目标远端主机。

3. **在远端主机上安装/升级**
   - 在远端 Ubuntu 上解压并执行安装或升级脚本/命令，完成 Cursor Server 的安装或升级。

## 禁止做法

- 不要在无法直连 Cursor 服务器的远端 Ubuntu 上直接运行会访问 Cursor 官网或 CDN 的安装/升级命令（例如直接下载并执行在线安装脚本），否则会因网络不可达而失败。
