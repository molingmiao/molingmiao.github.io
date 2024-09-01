---
layout: post
title:  "环境搭建：SDK安装"
categories: Flutter
tags: 环境搭建
author: MLM
---
# [1-1 安装软件]()

## [参考]()

- [Windows install](https://docs.flutter.dev/get-started/install/windows)
- [macOS install](https://docs.flutter.dev/get-started/install/macos)
- [Using Flutter in China](https://docs.flutter.dev/community/china)

## [git]()

git 代码版本控制

[https://git-scm.com/](https://git-scm.com/)

![](https://molingmiao.github.io/pic/d42f8c39b6dd9b9438b71925b7023907.png)

## [Android Studio]()

### [安装]()

官网

[https://developer.android.com/studio/index.html?hl=zh-cn](https://developer.android.com/studio/index.html?hl=zh-cn)

选择需要的版本下载，intel apple cpu 区分下

![](https://molingmiao.github.io/pic/91906fded32e7d25c1560013d07bb8b5.png)

首次安装需要去下载 sdk，一路默认就行，请打开加速，这个 dl.google.com 不太稳

![](https://molingmiao.github.io/pic/7592499760884a48648a6901e7f2fec3.png)

### [SDK 配置]()

点击 “SDK Manager”

![](https://molingmiao.github.io/pic/3e1f336e5f9ee4aaf18186b5e74a6d52.png)

SDK 列表, 可以先勾选个 Android 12 的，以后根据需要再加

![](https://molingmiao.github.io/pic/8bdd5638add304ce210f04ae82173742.png)

SDK Tools, 安装 command-line、x86 加速器

![](https://molingmiao.github.io/pic/f50260002c8c1c004c0121addbcb7d42.png)

## [XCode]()

### [安装]()

Apple Store 中升级到最新的 xcode

如果你原来的 xcode 很大，可以直接删除，装个新的

![](https://molingmiao.github.io/pic/bca896d06224a56937ca9b1ba69d93f2.png)

### [cocoapods]()

[https://cocoapods.org](https://cocoapods.org/)

![](https://molingmiao.github.io/pic/a5b77600074a3d83280810039e337b68.png)

```sh
$ sudo gem install cocoapods
```

M1 机器

```sh
$ sudo gem uninstall ffi && sudo gem install ffi -- --enable-libffi-alloc
```

### [配置 command-line]()

多个版本需要配置你的 xcode 主目录，默认不需要操作

```sh
$ sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
$ sudo xcodebuild -runFirstLaunch
```

### [同意 Xcode license]()

同意协议，默认不需要操作

```sh
$ sudo xcodebuild -license
```

## [Flutter SDK]()

### [压缩包方式]()

sdk 压缩包列表

[https://docs.flutter.dev/development/tools/sdk/releases?tab=macos](https://docs.flutter.dev/development/tools/sdk/releases?tab=macos)

![](https://molingmiao.github.io/pic/7efc5ba40819fdda04b325ee471db00a.png)

我现在用的 2.10.5 , v3 大家还是再等等

比如你解压到 `~/Documents/sdk/flutter`

### [环境变量]()

* macos

打开 `.bash_profile` 配置文件

```sh
$ vi ~/.bash_profile
```

写入配置

```sh
# flutter sdk
export PATH=${PATH}:~/Documents/sdk/flutter/bin

# dart sdk
export PATH=${PATH}:~/Documents/sdk/flutter/bin/cache/dart-sdk/bin
export PATH=${PATH}:~/.pub-cache/bin

# flutter-io 国内镜像
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn

# android
export ANDROID_HOME=~/Library/Android/sdk
export PATH=${PATH}:${ANDROID_HOME}/platform-tools
export PATH=${PATH}:${ANDROID_HOME}/tools
```

生效

```sh
$ source ~/.bash_profile
```

### [检查]()

```sh
$ flutter doctor
```

输出

```sh
$ flutter doctor
Flutter assets will be downloaded from https://storage.flutter-io.cn. Make sure you trust this source!
Running "flutter pub get" in flutter_tools...                       3.9s
Doctor summary (to see all details, run flutter doctor -v):
[✓] Flutter (Channel stable, 2.10.5, on macOS 12.3.1 21E258 darwin-x64, locale zh-Hans-CN)
[!] Android toolchain - develop for Android devices (Android SDK version 32.1.0-rc1)
    ✗ Android license status unknown.
      Run `flutter doctor --android-licenses` to accept the SDK licenses.
      See https://flutter.dev/docs/get-started/install/macos#android-setup for more details.
[✓] Xcode - develop for iOS and macOS (Xcode 13.4)
[✓] Chrome - develop for the web
[✓] Android Studio (version 2021.2)
[✓] VS Code (version 1.67.2)
[!] Proxy Configuration
    ! NO_PROXY does not contain ::1
[✓] Connected device ()
[✓] HTTP Host Availability

! Doctor found issues in 2 categories.
```

### [同意 Android Licenses]()

```sh
flutter doctor --android-licenses
```

### [windows 下设置]()

邮件 `我的电脑` -> `属性`

![](https://molingmiao.github.io/pic/7576a424900c729e3bd36ac06a771dc5.png)

点击 `高级系统设置`

![](https://molingmiao.github.io/pic/1898564b301ebd68ea38aa6064fadfd1.png)

点击 `环境变量`

![](https://molingmiao.github.io/pic/0f01a6f8ced87efa93d3789a2815daac.png)

参考 `macos` 下的属性进行添加修改

![](https://molingmiao.github.io/pic/d456353ebfbf8dbc36eabb9b777f7f20.png)

## [常见问题]()

* OS Error: Too many open files, errno = 24

```sh
$ ulimit -S -n 2048
```

* Pub failed to run subprocess `chmod`: ProcessException: Too many open files, Command: chmod 755 `/Users/ducafecat/Documents/sdk/flutter/.pub-cache/_temp/dirCGtulO/test/download-spec.sh`

```sh
chmod -R 755 /Users/ducafecat/Documents/sdk/flutter/
```

* Android sdkmanager not found. Update to the latest Android SDK and ensure that the cmdline-tools are installed to resolve this.

需要你去安装 Android 的 cmdline-tools

## [本节小结]()

本文概述了 Git、Android Studio、Xcode、CocoaPods 和 Flutter SDK 的安装配置过程。 主要介绍了各个工具的下载地址、安装步骤、环境变量设置等内容,并提供了解决常见问题的方法。
