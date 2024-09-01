---
layout: post
title:  "开发学习：vscode配置"
categories: Flutter
tags: 开发学习
author: MLM
---
# [vscode 配置]()

## [打开配置文件]()

命令行模式下 `cmd + shift + p`

![](https://molingmiao.github.io/pic/20220608155410.png)

## [配置 shell 下打开 code]()

输入 install code 搜索

![](https://molingmiao.github.io/pic/20220608155834.png)

## [自动应用提示]()

特别是大量的 `const` 提示警告

```js
  "editor.codeActionsOnSave": {
    "source.fixAll": true // 自动修复 all
  },
```

## [折叠配置文件]()

这样资源管理器文件列表就干净了

```js
  "explorer.fileNesting.enabled": true,
  "explorer.fileNesting.patterns": {
    "pubspec.yaml": ".packages, pubspec.lock, .flutter-plugins, .flutter-plugins-dependencies, .metadata, analysis_options.yaml, dartdoc_options.yaml"
  },
```

## [光标快速移动]()

设置键盘 “按键重复” “重复前延迟” ，这样打字快

![image-20220617061902456](https://molingmiao.github.io/pic/image-20220617061902456.png)

命令行中执行，关闭 vscode 苹果长按提示

```sh
$ defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool false
$ defaults write com.microsoft.VSCodeInsiders ApplePressAndHoldEnabled -bool false
```

## [括号线条高亮]()

全局设置

```
@id:editor.bracketPairColorization.enabled @id:editor.guides.bracketPairs
```

![image-20220620223132333](https://molingmiao.github.io/pic/image-20220620223132333.png)

![image-20220620223345020](https://molingmiao.github.io/pic/image-20220620223345020.png)
