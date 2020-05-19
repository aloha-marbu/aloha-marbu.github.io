---
title: Apple App内购买项目
date: 2020-04-10 16:48:23
tags: Apple Purchase
---

## 概述
您可通过 App 内购买项目销售各种内容，包括订阅、新功能和服务。您可提供四种类型的 App 内购买项目。用户可在 iOS、iPadOS、macOS、watchOS 及 Apple tvOS 设备上购买 App 内购买项目。

#### 消耗型项目
用户可以购买各种消耗型项目 (例如游戏中的生命或宝石) 以继续 app 内进程。消耗型项目只可使用一次，使用之后即失效，必须再次购买。

#### 非消耗型项目
用户可购买非消耗型项目以提升 app 内的功能。非消耗型项目只需购买一次，不会过期 (例如修图 app 中的其他滤镜)。Apple 可以[托管 (英文)](https://help.apple.com/app-store-connect/?lang=zh-cn#/dev1f52cd4dd?sub=dev456315af2) 您的非消耗型产品。

#### 自动续期订阅
用户可购买固定时段内的服务或更新的内容 (例如云存储或每周更新的杂志)。除非用户选择取消，否则此类订阅会自动续期。

#### 非续期订阅
用户可购买有时限性的服务或内容 (例如线上播放内容的季度订阅)。此类的订阅不会自动续期，用户需要逐次续订。

## 准备
在提供 App 内购买项目之前，您必须签署“Paid Applications Agreement (付费应用程序协议)”并设置好您的银行和税务信息。
[App Store Connect 帮助：协议、税务和银行业务概述 >](https://help.apple.com/app-store-connect/?lang=zh-cn#/devb6df5ee51)

#### 设置 Xcode 配置
使用 Xcode 来为您的 app 开启 App 内购买项目服务。
[Xcode 帮助: 为对象添加功能 (英文) >](https://help.apple.com/xcode/mac/current/#/dev88ff319e7)

#### 在 App Store Connect 上创建您的 App 内购买项目
在 App Store Connect 上配置您的 App 内购买项目，并为其提供详细信息，包括名称，价格，和能突显其功能的描述等。您也可以使用 XML 创建和管理您的 App 内购买项目。
[App Store Connect 帮助：创建 App 内购买项目 >](https://help.apple.com/app-store-connect/?lang=zh-cn#/devae49fb316)

## 设计和创建项目

#### 设计您的 App 内购买项目
您的 App 内购买项目的用户界面应当和 app 的整体相融合，并能有效带出您的产品的亮点。
[查看 Human Interface Guidelines (英文) >](https://developer.apple.com/design/human-interface-guidelines/in-app-purchase/overview/introduction/)

#### 实行您的 App 内购买项目
使用 StoreKit 框架，在您的 app 中实行 App 内购买项目，并安全地处理内容和服务的交易。 确保完成 implementation checklist (实行列表) 中的步骤。
[查看 API 文档 >](../StoreKit)

#### 验证收据
收据能提供十分有价值的销售记录。您可使用收据验证码来保护您的内容并防止未经授权的交易。
[App Store 收据 (英文)](https://developer.apple.com/documentation/appstorereceipts)
[App Store 服务器推送 (英文)](https://developer.apple.com/documentation/appstoreservernotifications)
[通过 App Store 验证收据](https://developer.apple.com/cn/documentation/storekit/in-app_purchase/validating_receipts_with_the_app_store)
[本地验证收据 (英文)](https://developer.apple.com/library/archive/releasenotes/General/ValidateAppStoreReceipt/Chapters/ValidateLocally.html#//apple_ref/doc/uid/TP40010573-CH1-SW2)

## 测试

#### 测试交易流程
使用 Apple 沙盒环境测试您的 App 内购买项目，而无需创建财务交易。
[App Store Connect 帮助：创建一个沙盒技术测试员帐户](https://help.apple.com/app-store-connect/?lang=zh-cn#/dev8b997bee1)
[App 内购买项目编程指南：测试步骤建议 (英文)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/StoreKitGuide/Chapters/ShowUI.html#//apple_ref/doc/uid/TP40008267-CH3-SW11)

#### 测试完整的用户体验
在 App Store 上发布您的 app 之前，使用 TestFlight 从大量用户中获取他们对您的 app 和 App 内购买项目提出的宝贵反馈。 在 App Store Connect 中邀请贵团队的用户，或向多达 10,000 名外部测试员的电子邮件地址发出邀请。 所有 App 内购买项目在 beta 测试期间都是免费的，但测试期结束后不可继续使用。


