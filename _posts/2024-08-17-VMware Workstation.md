---
layout: post
title:  "VMware Workstation"
categories: IOS模拟器
tags: VMware
author: MLM
---
因为想学ios编程，但是却没有苹果设备，没法使用xcode，虚拟机正好能解决他们的问题。

采用一键安装的方式来快速实现mac环境，原理上其实还是用了vm虚拟机。

把我已经安装好的mac系统，打包成vm备份恢复文件，省去了新建虚拟机和系统安装的过程，提高了安装成功的概率。

本次安装为了保证成功率和稳定性，选用了最成熟稳定的macOS Catalina 10.15.7，当然还有一个原因就是系统相对较小，打包下载容易一点。

## 环境准备：

安装前Ctrl+Alt+Del键打开任务管理器，在性能中查看cpu型号和虚拟化是否启用，AMD和intel的cpu在后续的安装步骤当中会有不同，假如虚拟化未启用，需要在开机进入bios界面设置开启，请自行百度你的主板品牌或者笔记本型号如何开启cpu虚拟化。

![](https://www.dhzy.fun/wp-content/uploads/41ecd32c72fe2ee.jpg)

## 1、安装vmware并解锁

### ·下载安装并激活

vmware Workstation 17

百度网盘：[https://pan.baidu.com/s/1xC4Zewn-67W2gpugVg79TQ?pwd=cjof ](https://pan.baidu.com/s/1xC4Zewn-67W2gpugVg79TQ?pwd=cjof ) 提取码：cjof

安装过程基本就是一直下一步，最后结束的时候使用下面的许可证密钥即可：

```
JU090-6039P-08409-8J0QH-2YR7F
```

\*注意：密钥只可用于个人测试，正式和商业使用需购买官方授权密钥

安装结束后，程序会提示重启一次电脑。

### ·解锁macos

解锁使用的是github开源程序unlocker：[https://github.com/DrDonk/unlocker/releases](https://github.com/DrDonk/unlocker/releases)

新版4系解锁失败的朋友可以试试我保存的旧版3系解锁工具：

阿里云盘：[https://www.aliyundrive.com/s/w3fM4jaZMjk](https://www.aliyundrive.com/s/w3fM4jaZMjk) 提取码：qZ4N

百度网盘：[https://pan.baidu.com/s/1KV7Y5MBghnnKwYlKZ0Ycow?pwd=ie76](https://pan.baidu.com/s/1KV7Y5MBghnnKwYlKZ0Ycow?pwd=ie76) 提取码：ie76

解锁涉及到修改注册列表，会报毒，请先关闭杀毒软件

解锁前需要关闭vmvare程序，同时关闭任务管理器中所有vm开头的服务

\*注意：解锁成功后，将vm开头的服务重新开启，否则macos无法联网

![](https://www.dhzy.fun/wp-content/uploads/2bd4bab82a60942.jpg)

将解锁包解压出来，右键以管理员身份运行win-install.cmd

\*注意：还有一种说法是需要将解锁文件夹放到vmware安装根目录运行，解锁失败的的朋友可以尝试。

\*注意：解锁不成功的可以尝试另一个解锁工具auto-unlocker：[https://github.com/paolo-projects/auto-unlocker/releases](https://github.com/paolo-projects/auto-unlocker/releases)

解锁成功的标志就是虚拟机中新建虚拟机第三步有了macos的选项。

![](https://www.dhzy.fun/wp-content/uploads/677ad4cffde836c.jpg)

## 2、导入macos10.15虚拟机包

---

**macOS虚拟机打包下载**

[![虚拟机一键安装苹果系统macos10.15，windows轻松解决xcode环境](https://www.dhzy.fun/wp-content/themes/ripro-v2/timthumb.php?src=https://www.dhzy.fun/wp-content/uploads/723f90a315950bc.jpg&w=300&h=200&zc=1&a=c&q=90)](https://www.dhzy.fun/archives/3889.html "[免费]MacOS Catalina 10.15.7 苹果镜像vmware虚拟机一键安装vmdk文件打包下载")

##### [[免费]MacOS Catalina 10.15.7 苹果镜像vmware虚拟机一键安装vmdk文件打包下载](https://www.dhzy.fun/archives/3889.html "[免费]MacOS Catalina 10.15.7 苹果镜像vmware虚拟机一键安装vmdk文件打包下载")

注意：本镜像由大海制作，并且免费提供，但由于是市场紧俏资源，很多人会拿来卖钱，希望拿到本镜像的朋友尽量免费分...

**推荐** 2022-03-19

---

### ·修改vmx文件

先把打包的macos10.15解压出来，右键打开方式记事本编辑macOS 10.15.vmx文件并保存（这里看不到.vmx后缀的，查看-显示-文件扩展名）

根据自己的cpu类型添加修改代码，每个人的环境不同，我这里给出几种方案，假如一种失败，请切换尝试，修改前务必关闭虚拟机再更改。

假如还不行，死马当活马医iner和amd的代码可交换尝试。

\*注意：切换新代码把修改过的地方先复原，不要套娃。

#### intel的cpu：

（1）不修改

（2）结尾处添加代码

```
smc.version = 0
```

（3）结尾处添加代码

```
smc.version = "0"
cpuid.0.eax = "0000:0000:0000:0000:0000:0000:0000:1011"
cpuid.0.ebx = "0111:0101:0110:1110:0110:0101:0100:0111"
cpuid.0.ecx = "0110:1100:0110:0101:0111:0100:0110:1110"
cpuid.0.edx = "0100:1001:0110:0101:0110:1110:0110:1001"
cpuid.1.eax = "0000:0000:0000:0001:0000:0110:0111:0001"
cpuid.1.ebx = "0000:0010:0000:0001:0000:1000:0000:0000"
cpuid.1.ecx = "1000:0010:1001:1000:0010:0010:0000:0011"
cpuid.1.edx = "0000:1111:1010:1011:1111:1011:1111:1111"
featureCompat.enable = "FALSE"
```

（4）结尾处添加代码

```
smc.version = "0"
cpuid.0.eax = "0000:0000:0000:0000:0000:0000:0000:1011"
cpuid.0.ebx = "0111:0101:0110:1110:0110:0101:0100:0111"
cpuid.0.ecx = "0110:1100:0110:0101:0111:0100:0110:1110"
cpuid.0.edx = "0100:1001:0110:0101:0110:1110:0110:1001"
cpuid.1.eax = "0000:0000:0000:0001:0000:0110:0111:0001"
cpuid.1.ebx = "0000:0010:0000:0001:0000:1000:0000:0000"
cpuid.1.ecx = "1000:0010:1001:1000:0010:0010:0000:0011"
cpuid.1.edx = "0000:1111:1010:1011:1111:1011:1111:1111"
featureCompat.enable = "TRUE"
```

（5）结尾处添加代码

```
smbios.reflectHost = "TRUE"
hw.model = "MacBookPro16,1"
board-id = "Mac-E1008331FDC96864" 
```

#### amd的cpu：

（1）不修改

（2）结尾处添加代码

```
smc.version = "0"
cpuid.0.eax = "0000:0000:0000:0000:0000:0000:0000:1011"
cpuid.0.ebx = "0111:0101:0110:1110:0110:0101:0100:0111"
cpuid.0.ecx = "0110:1100:0110:0101:0111:0100:0110:1110"
cpuid.0.edx = "0100:1001:0110:0101:0110:1110:0110:1001"
cpuid.1.eax = "0000:0000:0000:0001:0000:0110:0111:0001"
cpuid.1.ebx = "0000:0010:0000:0001:0000:1000:0000:0000"
cpuid.1.ecx = "1000:0010:1001:1000:0010:0010:0000:0011"
cpuid.1.edx = "0000:0111:1000:1011:1111:1011:1111:1111"
smbios.reflectHost = "TRUE"
hw.model = "MacBookPro14,3"
board-id = "Mac-551B86E5744E2388"
keyboard.vusb.enable = "TRUE"
mouse.vusb.enable = "TRUE"
```

（3）结尾处添加代码

```
smc.version = "0"
cpuid.0.eax = "0000:0000:0000:0000:0000:0000:0000:1011"
cpuid.0.ebx = "0111:0101:0110:1110:0110:0101:0100:0111"
cpuid.0.ecx = "0110:1100:0110:0101:0111:0100:0110:1110"
cpuid.0.edx = "0100:1001:0110:0101:0110:1110:0110:1001"
cpuid.1.eax = "0000:0000:0000:0001:0000:0110:0111:0001"
cpuid.1.ebx = "0000:0010:0000:0001:0000:1000:0000:0000"
cpuid.1.ecx = "1000:0010:1001:1000:0010:0010:0000:0011"

cpuid.1.edx = "0000:0111:1000:1011:1111:1011:1111:1111"
```

（4）结尾处添加代码

```
smc.version = "0"
cpuid.0.eax = "0000:0000:0000:0000:0000:0000:0000:1011"
cpuid.0.ebx = "0111:0101:0110:1110:0110:0101:0100:0111"
cpuid.0.ecx = "0110:1100:0110:0101:0111:0100:0110:1110"
cpuid.0.edx = "0100:1001:0110:0101:0110:1110:0110:1001"
cpuid.1.eax = "0000:0000:0000:0001:0000:0110:0111:0001"
cpuid.1.ebx = "0000:0010:0000:0001:0000:1000:0000:0000"
cpuid.1.ecx = "1000:0010:1001:1000:0010:0010:0000:0011"
cpuid.1.edx = "0000:0111:1000:1011:1111:1011:1111:1111"
featureCompat.enable = "TRUE"
```

### 关于vmx文件修改的其他问题参考：

（1）如果虚拟机开机一直无限重启 可以在那个vmx加上这样的一行

```
cpuid.1.eax = "0000:0000:0000:0001:0000:0110:1010:0101"
```

（2）VMware Workstation不可恢复错误，在smc.present = “TRUE”这行的后面一行加上代码：smc.version = 0

![](https://www.dhzy.fun/wp-content/uploads/5602133285261cb.jpg)

（3）无法打开内核设备“\\\\.\\VMCIDev\\VMX”: 重叠 I/O 操作在进行中。你想要在安装 VMware Workstation 前重启吗?

找到这一行： vmci0.present = "TRUE"，将 TRUE 改为 FALSE，或者 直接将这行删除。

### ·导入macOS 10.15

vm中选择打开虚拟机，找到解压后的文件夹，选择macOS 10.15.vmx打开

![](https://www.dhzy.fun/wp-content/uploads/e8711197fe12192.jpg)

开启此虚拟机，开始享受你的macos吧，开机密码：dhzy

![](https://www.dhzy.fun/wp-content/uploads/25d6c0d5f8d1c14.jpg)
