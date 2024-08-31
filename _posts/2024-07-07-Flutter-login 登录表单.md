---
layout: post
title:  "开发学习：login 登录表单"
categories: Flutter
tags: 布局练习
author: MLM
---
## [目标]()

* 编写表单
* 有效性检查

![image-20220622220331169](https://molingmiao.github.io/tag/image-20220622220331169.png)

## [登录表单]()

lib/pages/login.dart

```dart
  // 账号输入是否有效
  bool isUserNameValid = false;
```

```dart
  // 登录表单
  Widget _buildForm() {
    return Container(
      padding: const EdgeInsets.fromLTRB(20, 50, 20, 20),
      decoration: BoxDecoration(
        color: Colors.white,
        borderRadius: BorderRadius.circular(35),
      ),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          // Username or E-Mail
          const Text(
            "Username or E-Mail",
            style: TextStyle(
              fontSize: 15,
              color: Color(0xff838383),
              fontWeight: FontWeight.w300,
            ),
          ),
          TextField(
            onChanged: (value) {
              bool valid = false;
              if (value.length >= 6) {
                valid = true;
              } else {
                valid = false;
              }

              setState(() {
                isUserNameValid = valid;
              });
            },
            decoration: InputDecoration(
              hintText: "@",
              // labelText: "Username or E-Mail",
              // labelStyle: const TextStyle(
              //   fontSize: 15,
              //   color: Color(0xff838383),
              //   fontWeight: FontWeight.w300,
              // ),
              prefixIcon: Image.asset(
                AssetsImages.iconUserPng,
                width: 23,
                height: 23,
              ),
              suffixIcon: isUserNameValid == true
                  ? const Icon(
                      Icons.done,
                      color: Colors.green,
                    )
                  : null,
            ),
          ),

          // 间距
          const SizedBox(height: 35),

          // Password
          const Text(
            "Password",
            style: TextStyle(
              fontSize: 15,
              color: Color(0xff838383),
              fontWeight: FontWeight.w300,
            ),
          ),
          TextField(
            obscureText: true,
            decoration: InputDecoration(
              hintText: "6 digits",
              // labelText: "Password",
              // labelStyle: const TextStyle(
              //   fontSize: 15,
              //   color: Color(0xff838383),
              //   fontWeight: FontWeight.w300,
              // ),
              prefixIcon: Image.asset(
                AssetsImages.iconLockPng,
                width: 23,
                height: 23,
              ),
              suffixIcon: TextButton(
                onPressed: () {},
                child: const Text(
                  "Forget?",
                  style: TextStyle(
                    fontSize: 15,
                    color: Color(0xff0274bc),
                    fontWeight: FontWeight.w500,
                  ),
                ),
              ),
            ),
          ),

          // 间距
          const SizedBox(height: 30),

          // Sign In

          // 间距
          const SizedBox(height: 16),

          // Don’t have an account?  + Sign Up
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              // 文字
              const Text(
                "Don’t have an account? ",
                style: TextStyle(
                  fontSize: 15,
                  color: Color(0xff171717),
                  fontWeight: FontWeight.w300,
                ),
              ),
            
              // 按钮
              TextButton(
                onPressed: () {},
                child: const Text(
                  "Sign Up",
                  style: TextStyle(
                    fontSize: 15,
                    color: Color(0xff0274bc),
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
            
            ],
          ),
        ],
      ),
    );
  }
```

## [总结]()

* 通过 `TextField.decoration` 属性进行装饰
* `TextField.obscureText` 开启密码
