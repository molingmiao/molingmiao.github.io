---
layout: post
title:  "环境搭建：FVM版本管理"
categories: Flutter
tags: 环境搭建
author: MLM
---
# [1-3 fvm版本管理]()

## [参考]()

* [fvm.app](https://fvm.app/)
* [sidekick](https://github.com/fluttertools/sidekick)

![](https://molingmiao.github.io/pic/0666887ccae4f68ae2b57dc5e7966cc3.png)

## [特点]()

* 系统全局版本切换
* 不同项目间可以多个版本切换
* 支持桌面工具、cli 命令行、Docker 方式

## [安装]()

* 安装 fvm

```sh
brew tap leoafarias/fvm
brew install leoafarias/fvm/fvm
```

* 安装 sdk

```sh
fvm install 2.10.5
```

* 设置全局

```
fvm global 2.10.5
```

* 修改环境变量

```sh
code ~/.bash_profile

# flutter sdk
export PATH=${PATH}:~/fvm/default/bin

# dart sdk
export PATH=${PATH}:~/fvm/default/bin/cache/dart-sdk/bin
export PATH=${PATH}:~/.pub-cache/bin
```

* vscode 配置

默认个情况 vscode 会从你的 PATH 中读取 sdk 位置，如果还是提示找不到，可以如下操作：

开设置`setting.json` 面板，加入 fvm 的默认位置

```json
"dart.flutterSdkPath": "~/fvm/default/bin"
```

* Android studio 设置

打开项目属性面板

```
~/fvm/default/bin
```

## [全局切换]()

* 安装 3.0.1

```sh
fvm install 3.0.1
```

* 设置当前默认

```sh
fvm global 3.0.1
```

## [项目单独版本]()

* 进入项目目录

```sh
fvm use 3.0.1
```

* vscode sdk 搜索

编辑 `.vscode/settings.json`

```json
{
  "dart.flutterSdkPath": ".fvm/flutter_sdk",
  // Remove .fvm files from search
  "search.exclude": {
    "**/.fvm": true
  },
  // Remove from file watching
  "files.watcherExclude": {
    "**/.fvm": true
  }
}
```

* Android Studio 忽略搜索目录

修改 `.idea/workspace.xml`

```xml
<component name="VcsManagerConfiguration">
  <ignored-roots>
    <path value="$PROJECT_DIR$/.fvm/flutter_sdk" />
  </ignored-roots>
</component>
```

* Android Studio 调整 sdk 位置

![](https://molingmiao.github.io/pic/349ad5029c69d28008c9a632b302e67c.png)

## [Git 忽略 `fvm/flutter_sdk`]()

编辑 `.gitignore`

```sh
.fvm/flutter_sdk
```

## [其它]()

* 卸载

```sh
brew uninstall leoafarias/fvm/fvm
brew untap leoafarias/fvm
```

* 删除 sdk

```sh
fvm remove 2.10.5
```

* 已安装的 sdk 列表

```sh
fvm list
```

* 查看可安装的 sdk 版本

```sh
fvm release
```

* 检查环境

```
fvm docctor
```

## [Sidekick 桌面应用]()

[https://github.com/fluttertools/sidekick](https://github.com/fluttertools/sidekick)

![](https://molingmiao.github.io/pic/daec09b264e5c2e562fd19dc58cbf0db.png)

* 安装

[https://github.com/fluttertools/sidekick/releases](https://github.com/fluttertools/sidekick/releases)

* 图形界面操作

![](https://molingmiao.github.io/pic/4e8d353d7b537a6b3e8f83308484747f.png)

* 可设置中文

![](https://molingmiao.github.io/pic/b7e144541dc310014a33dcd4698fff64.png)

## [常见问题]()

* Error: Formulae found in multiple taps: \_ befovy/taps/fvm \_ leoafarias/fvm/fvm

那我们指定安装 leoafarias/fvm/fvm

```sh
brew install leoafarias/fvm/fvm
```

* OS Error: Too many open files, errno = 24

临时扩大线程栈空间

```sh
ulimit -S -n 2048
```

* GitHub API Error: Bad credentials (GitHub::API::AuthenticationFailedError) The GitHub credentials in the macOS keychain may be invalid.

提示

```
Clear them with:
  printf "protocol=https\nhost=github.com\n" | git credential-osxkeychain erase
Create a GitHub personal access token:
    https://github.com/settings/tokens/new?scopes=gist,repo,workflow&description=Homebrew
  echo 'export HOMEBREW_GITHUB_API_TOKEN=your_token_here' >> ~/.zshrc
```

我这边是建了 token 然后零时设置了

![](https://molingmiao.github.io/pic/65b6573e9fc14a87f8b08760acdb4356.png)

```sh
export HOMEBREW_GITHUB_API_TOKEN=ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

## [本节小结]()

FVM 是一个简单的管理和切换不同 Flutter 版本的软件。

Flutter 开发工具 Sidekick，它可以帮助开发者更愉快地进行 Flutter 开发。它主要提供了以下功能:

1. 管理和切换不同 Flutter 版本
2. 支持桌面工具、命令行和 Docker 等方式安装
3. 提供全局和项目级别的 Flutter SDK 版本切换
4. 集成了 Android Studio 和 VS Code 的设置
5. 提供了易用的图形界面操作
