---
layout: post
title:  "开发学习：login 按钮抽取"
categories: Flutter
tags: 布局练习
author: MLM
---
# [3.3 login 按钮抽取]()

## [目标]()

* 抽取公共按钮组件
* 修改成纯 `ElevatedButton` 按钮

![image-20220622222415206](https://molingmiao.github.io/pic/image-20220622222415206.png)

## [按钮组件抽取]()

lib/common/widgets.dart

```dart
import 'package:flutter/material.dart';

/// 按钮组件
class ButtonWidget extends StatelessWidget {
  const ButtonWidget({
    Key? key,
    this.height,
    this.widget,
    this.radius,
    this.onPressed,
    this.text,
  }) : super(key: key);

  /// 文字
  final String? text;

  /// 高度
  final double? height;

  /// 宽度
  final double? widget;

  /// 圆角
  final double? radius;

  /// 点击事件
  final void Function()? onPressed;

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: onPressed,
      style: ButtonStyle(
        // 阴影高度
        elevation: MaterialStateProperty.all(0),
        // 最小尺寸
        minimumSize: MaterialStateProperty.all(
            Size(widget ?? double.infinity, height ?? double.infinity)),
        // 形状 圆角
        shape: MaterialStateProperty.all(
          RoundedRectangleBorder(
            borderRadius: BorderRadius.all(
              Radius.circular(radius ?? 18),
            ),
          ),
        ),
      ),
      child: Text(
        // 文字
        text ?? "",
        // 文字样式
        style: const TextStyle(
          fontSize: 16,
          fontWeight: FontWeight.w300,
          color: Colors.white,
        ),
      ),
    );
  }
}
```

## [登录按钮]()

lib/pages/login.dart

```dart
  // 登录表单
  Widget _buildForm() {
                    ...
                // Sign In
          ButtonWidget(
            text: 'Sign In',
            onPressed: () {},
            height: 60,
            widget: double.infinity,
            radius: 18,
          ),
```

## [欢迎按钮]()

lib/pages/welcome.dart

```dart
  // 底部按钮
  Padding _buildBtns(BuildContext context) {
    ...
    // Get Started
    ButtonWidget(
      text: "Get Started",
      height: 42,
      widget: 140,
      radius: 32,
      onPressed: () => onLogin(context),
    ),
```

```dart
  // goto 登录页面
  void onLogin(BuildContext context) {
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => const LoginPage()),
    );
  }
```

## [总结]()

* 公共组件类抽取方法
* `ElevatedButton` 组件属性配置
