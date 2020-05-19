---
title: iOS Universal links 配置
date: 2020-03-30 17:45:03
tags: UniversalLinks iOS 
---

通常我们在跳转到其他app时使用的是`scheme url`的方式，但是现在在申请微信登录或者qq登录时，都开始要求设置`Universal Links`。
[通用链接](https://developer.apple.com/library/archive/documentation/General/Conceptual/AppSearch/UniversalLinks.html#//apple_ref/doc/uid/TP40016308-CH12-SW1)

## 一、苹果开发者账号配置
#### 1. `Account` -> `Identifiers` 打开`Associated Domains`开关
#### 2. 保存`App ID Prefix(Team ID)`和`Bundle ID`后面配置文件要用到
![](appledeveloperid.png)

## 二、网站配置
#### 1. 创建配置文件
新建一个名字为`apple-app-site-association`的纯文本文件(这里就用到之前保存的两个ID)，不要有任何后缀，文件内容为
```
{
    "applinks": {
        "apps": [],
        "details": [
            {
                "appID": "TeamID.BundleID",
                "paths": [ "限制的域名"]
            }
        ]
    }
}
```
- `apps`这个字段保持为空数组即可
- `details`是指定哪个页面用哪个`App`打开的数组，如果你有多个路径指定不同的`App`，按照上面的规则在`details`下添加对应的`appID`和`paths`即可。
- `appID`就是`Team ID`.`Bundle ID`
- `paths`路径可以参考
    1. 这个paths路径的更多限制规则可以参考下面
    2. 包含特定的网址（例如/wwdc/news/）以指定特定的链接
    3. 附加到特定的网址（例如/videos/wwdc/2015/）以指定网站的一部分
    4. 除了用于匹配任何子字符串之外，您还可以?用于匹配任何单个字符。您可以将两个通配符合并在一个路径中，例如/foo//bar/201?/mypage。
    5. 路径字符串的开头添加NOT指定不应作为通用链接处理的区域，例如"paths": [ "/videos/wwdc/201?/" , "NOT /videos/wwdc/2010/"]

比如你`Team ID`是`ASDFG12345`，`Bundle ID`是`com.marbu.blog`，只在
访问`https://www.aloha-marbu.com/app/`链接时才显示顶部的用app打开，其他网站层次不显示，那么这个文件的内容就是
```
{
    "applinks": {
        "apps": [],
        "details": [
            {
                "appID": "ASDFG12345.com.marbu.blog",
                "paths": [ "/app/*"]
            }
        ]
    }
}
```
然后将这个文件上传到网站根目录，或者在根目录新建一个名字为`.well-known`的子目录，然后把这个文件上传到这个子目录中。**注意：网站域名必须支持https**

#### 2.网站验证
上传之后，可以访问[https://search.developer.apple.com/appsearch-validation-tool/](https://search.developer.apple.com/appsearch-validation-tool/)，苹果专门提供的验证工具，然后将域名网址填进去，例如`www.aloha-marbu.com/`，然后点击测试。

![](applevalidation.png)

## 三、Xcode配置
1. 打开工程配置中的Associated Domains

`TARGETS` -> `Your TARGET` -> `Signing & Capabilities` -> `Associated Domains`
![](xcodeassociateddomains.png)
2. 添加网站域名

网站域名以`applinks:`开头，后面是你放`apple-app-site-association`文件的域名，比如：`applinks:www.aloha-marbu.com`

## 四、测试
一切配置完成之后，删除你的`App`（只有删除重装Apple才会从你的服务器请求你的配置文件）
在`Safari`中打开`域名/配置的path`，拿之前的例子就应该是`https://www.aloha-marbu.com/app/`，然后页面往下拉，如果有有你`App`跳转相关信息，那么恭喜你成功了，没有也不要慌，确认配置无误的话，等一会再试试。



