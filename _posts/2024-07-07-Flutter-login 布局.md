---
layout: post
title:  "开发学习：login 布局"
categories: Flutter
tags: 布局练习
author: MLM
---
# [3.1 login 布局]()

## [目标]()

* 看标注布局界面（千锤百炼）

![image-20220622212914896](https://molingmiao.github.io/tag/image-20220622212914896.png)

## [布局]()

lib/pages/login.dart

```dart
  // 登录表单
  Widget _buildForm() {
    return Container();
  }
```

```dart
    // 主视图
  Widget _buildView() {
    return Container(
      padding: const EdgeInsets.symmetric(horizontal: 15),
      color: AppColors.backgroundSplash,
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          // 图标
          Image.asset(
            AssetsImages.logoPng,
            width: 60,
          ),

          const SizedBox(height: 20),

          // 主标
          const Text(
            "Let’s Sign You In",
            style: TextStyle(
              fontSize: 20,
              color: Colors.white,
              fontWeight: FontWeight.bold,
            ),
          ),

          const SizedBox(height: 10),

          // 子标
          const Text(
            "Welcome back, you’ve been missed!",
            style: TextStyle(
              fontSize: 13,
              color: Colors.white,
              fontWeight: FontWeight.w300,
            ),
          ),

          const SizedBox(height: 50),

          // 表单
          _buildForm(),
        ],
      ),
    );
  }
```

```dart
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: _buildView(),
    );
  }
```

## [总结]()

* 记住布局规则 “从上往下、从左往右”
* 用函数拆分视图结构
