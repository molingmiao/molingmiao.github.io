---
layout: post
title:  "Flutter学习中的问题：VScode中提交Github的问题"
categories: Flutter
tags: github提交
author: MLM
---

#### 摘要

在这篇技术博客中，我们将深入探讨如何解决**Git**在连接**GitHub**时遇到的“Failed to connect to github.com port 443 after 21090 ms: Couldn‘t connect to server”错误。本文适合各级别读者，无论你是编程新手还是经验丰富的开发者，都能从中获益。通过SEO优化，本文包含关键词如Git, GitHub, 端口443, [VPN](https://cloud.tencent.com/product/vpn?from_column=20065&from=20065), 代理设置等，旨在帮助更多遇到相同问题的朋友。

#### 引言

大家好，我是猫头虎博主，今天我们要聊的是Git连接问题。作为开发者，我们经常需要使用Git来管理项目代码。但是，有时候在连接GitHub时会遇到一些棘手的问题，比如端口443连接失败。本文将详细介绍如何解决这个问题，让你的代码管理之路更加顺畅。🚀

#### 正文

##### 一、遇到问题时的背景分析 🤔

当你在使用Git与GitHub交互时，可能会遇到这样的错误信息：“Failed to connect to github.com port 443 after 21090 ms: Couldn‘t connect to server”。这通常发生在使用VPN后，系统端口号与Git端口号不一致时。

##### 二、解决步骤详解 🛠️

###### 1. 问题定位

首先，确认你是否在使用VPN。VPN的使用可能会改变本机的系统端口号，从而影响到Git的正常连接。

###### 2. 操作指南

###### a. VPN使用环境下的解决方案

**查看系统端口号**:  打开“设置 -> 网络和Internet -> 代理”，记录下当前的端口号。

**设置Git端口号**:  使用命令：

**代码语言：**javascript

**复制**

```javascript
git config --global http.proxy 127.0.0.1:<你的端口号>
git config --global https.proxy 127.0.0.1:<你的端口号>
```

例如，如果你的端口号是10809，则输入：

**代码语言：**javascript

**复制**

```javascript
git config --global http.proxy 127.0.0.1:10809
git config --global https.proxy 127.0.0.1:10809
```

**验证设置** (可选):

**代码语言：**javascript

**复制**

```javascript
git config --global -l
```

检查输出，确认代理设置已正确配置。

**重试Git操作**:  在执行`git push`或`git pull`前，建议在命令行中运行`ipconfig/flushdns`以刷新**DNS**缓存。

###### b. 未使用VPN时的解决方案

如果你并未使用VPN，但依然遇到端口443连接失败的问题，尝试取消Git的代理设置：

**代码语言：**javascript

**复制**

```javascript
git config --global --unset http.proxy
git config --global --unset https.proxy
```

之后重试Git操作，并刷新DNS缓存。

##### 三、小结 📝

我们讨论了两种常见场景下Git连接GitHub时遇到端口443错误的情况及其解决方法。重点在于检查和调整代理设置，以保证Git可以顺利连接到GitHub。
