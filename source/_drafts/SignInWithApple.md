---
title: Sign in with Apple
date: 2020-03-16 17:45:03
tags: Sign Apple iOS 
---
## 摘要
`iOS 13`新增功能，支持`iOS`、`macOS`、`watchOS`、`tvOS`和`Web`，苹果对所有接入了第三方登录的App，要求接入`Sign in with Apple`。从2019-9-12起，提交到**App Store**的新应用必须遵守，现有应用必须在2020年4月之前进行相关更新。

## 说明
- `Sign in with Apple`为用户提供一种快速安全的登录方式, 用户可以轻松登录开发者的应用和网站
- 使用`Apple`登录可以让用户在系统中设置用户帐户，开发者可以获取到用户名称(`Name`), 用户唯一标识符(`ID`)以及经过验证的电子邮件地址(`email`)

## 特性
- 尊重用户隐私：开发人员仅仅只能获取到用户的姓名和邮箱, 苹果也不会收集用户和应用交互的任何信息
- 系统内置的安全性：`2F`双重验证(`Face ID`或T`ouch ID`)，从此登录不再需要密码
- 简化账号的创建和登录流程，无缝跨设备使用
- 开发者可以获取到已验证过的邮箱作为登录账号或者与用户进行通信（注：用户可以选择隐藏真实邮箱，并使用苹果提供的虚拟邮箱进行授权）
- 更多前往[Apple Developer](https://developer.apple.com/sign-in-with-apple/)查看

## 开始

##### 准备工作
- 在开发者网站，[添加Sign in with Apple功能](https://developer.apple.com/account/)
- 在`Xcode`中开启`Sign in with Apple`功能

##### 开始编码
1. 导入框架`import AuthenticationServices`
2. 登录按钮
- 系统提供的登录按钮
```
@available(iOS 13.0, *)
open class ASAuthorizationAppleIDButton : UIControl {
    // 初始化方法
    public convenience init(type: ASAuthorizationAppleIDButton.ButtonType, style: ASAuthorizationAppleIDButton.Style)

    // ..
    public init(authorizationButtonType type: ASAuthorizationAppleIDButton.ButtonType, authorizationButtonStyle style: ASAuthorizationAppleIDButton.Style)

    // 按钮圆角
    open var cornerRadius: CGFloat
}
```

- 自定义登录按钮










