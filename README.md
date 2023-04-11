<img src="https://avatars.githubusercontent.com/u/121547934?s=144">

[![version](https://img.shields.io/badge/dawn-v1.0.0-yellow)]()
</br>
[![version](https://img.shields.io/badge/EventTracing-iOS-green)]()
[![version](https://img.shields.io/badge/EventTracing-Android-green)]()
[![version](https://img.shields.io/badge/EventTracing-web-green)]()
</br>
[![version](https://img.shields.io/badge/easyinsight-server-blue)]()
[![version](https://img.shields.io/badge/easyinsight-front-blue)]()

# 曙光

**曙光埋点** 是一套全链路埋点方案，从埋点设计、到客户端三端(iOS、Android、H5)开发、以及埋点校验&稽查、再到埋点数据使用，目前已经广泛应用于云音乐各个主要APP，它集自动化埋点与全链路追踪等特点于一身，近乎完美地解决了传统埋点的所有痛点，兼顾了开发效率与埋点数据的高精度特点。

[云音乐曙光埋点：还原数据理想国](https://mp.weixin.qq.com/s/4Wq4nj-oQPohMqmQv_Pe9g)

## 为什么用曙光

相比同类竞品的方案，曙光埋点有如下优势

- **规范化**: 客户端开发时，格式、参数(公共参数、SDK保留参数、参数类型/格式等)、**埋点时机**，双端规范统一化，可无缝对接H5、RN等
- **链路追踪**: 全链路级别的链路追踪能力，助力绘制用户画像，满足你漏斗分析、个性化推荐、实时分析、离线分析
- **对象化-虚拟树VTree**: 从埋点录入人员，到客户端埋点开发人员，我们面向的是一个个的对象
- **埋点数据管理**: 埋点虚拟树、埋点对象的可视化管理，涵盖着多版本并行开发管理，告别埋点管理混乱
- **埋点校验&稽查**: 线下埋点校验，和线上买点稽查，同时配备了可供开发/测试方便的客户端层面的可视化工具，保障埋点质量

## 曙光包含哪些
- iOS SDK
- Android SDK
- H5 SDK（可用于站内/站外）
- Easyinsight埋点管理平台

## 工程介绍

这个是一个容器级别的壳子工程，以 git submodule 的形式管理其他子项目，子项目包括如下：

- **iOS SDK**: [EventTracing-iOS](https://github.com/eventtracing/EventTracing-iOS), Debug工具 [EventTracing-iOS-Debug](https://github.com/eventtracing/EventTracing-iOS-Debug), 埋点校验工具 [EventTracing-iOS-LogViewer](https://github.com/eventtracing/EventTracing-iOS-LogViewer)
- **Android SDK**: [EventTracing-Android](https://github.com/eventtracing/EventTracing-Android)
- **H5 SDK**: [EventTracing-web](https://github.com/eventtracing/EventTracing-web)
- **埋点平台 easyinsight-server**: [easyinsight-server](https://github.com/eventtracing/easyinsight-server)
- **埋点平台 easyinsight-front**: [easyinsight-front](https://github.com/eventtracing/easyinsight-front)

## iOS & Android端侧SDK特点
### 轻量

曙光端侧SDK非常轻量，代码里只有数千行，对APP包体积占用非常小，对原有业务也不会增加额外的负担，这一点在云音乐等业内非常成熟的产品环境得到有力验证。它的接入也十分简单，您只需要根据下述文档即可在很短时间内完成功能的接入与使用。

### 自动埋点

曙光支持常见事件的自动打点，包括`点击`、`曝光`、`滚动`等。
![event product](https://user-images.githubusercontent.com/121547934/217256651-38c9aba7-4f0f-4cc2-af3e-200883ffdffa.png)

### 链路追踪

几乎全自动的链接追踪，开发人员几乎不需要额外的工作，强大又简单。 有关链接跟踪原理的更多介绍，请参阅以下文档
**[Link Tracking Introduction](https://eventtracing.github.io/docs/category/%E9%93%BE%E8%B7%AF%E8%BF%BD%E8%B8%AA)**

### 模块架构
![arch](https://user-images.githubusercontent.com/121547934/217257118-ec2e7658-7093-474a-811d-ee173a7e607e.png)

## 使用曙光

- **[官方Demo](https://eventtracing.github.io/docs/category/%E5%AE%98%E6%96%B9demo)** 包含常见场景的使用演示，以及丰富的单元测试
- **[快速开始](https://eventtracing.github.io/docs/category/%E5%AE%98%E6%96%B9demo)** 包含基本场景的SDK接入，以及简单场景的使用
- **[曙光接入](https://eventtracing.github.io/docs/category/%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B)** 包含详细的接入手册，以及各项能力解析
- SDK的详细使用，参见 [iOS SDK详细使用](https://eventtracing.github.io/docs/category/ios)，[Android SDK详细使用](https://eventtracing.github.io/docs/category/android)，[H5 SDK详细使用](https://eventtracing.github.io/docs/category/h5--rn)

### 全局配置

#### 引入 SDK

> iOS

**使用 cocoapods 接入**

```ruby
# 埋点SDK
pod 'EventTracing-iOS'

# 调试工具
pod 'EventTracing-iOS-Debug', :configurations => ["Debug"]
# 埋点校验工具
pod 'EventTracing-iOS-LogViewer', :configurations => ["Debug"]
```

> Android

**build.gradle(project)**

```groovy
buildscript {
    repositories {
        ........
        maven {
            url './repo'
        }
    }
    dependencies {
        .......
        classpath "com.netease.cloudmusic.plugin:datareport-plugin:1.0.0"
    }
}
```

**build.gradle(app)**

```groovy
......
apply plugin: 'datareport-plugin'

dataReportConfig {
    targetPackages = ['androidx/appcompat', 'androidx/recyclerview/widget', 'androidx/viewpager/widget','com/netease/datareport/demo']
    excludePackages = []
    openDebugLog = true
}

dependencies {
    ......
    implementation project(':datareport')
    implementation project(':datareport_debug')
}
```

#### SDK 初始化

曙光埋点的启动十分简单，您只需要在APP启动时的合适时机（比如 `didFinishLaunch`加入如下代码，进行一些简单配置，即可完成SDK的启动

> iOS
```objc
   [[EventTracingEngine sharedInstance] startWithContextBuilder:^(id<EventTracingContextBuilder> _Nonnull builder) {
       // output channel
       [builder addOutputChannel:self];
   }];
```
> Android
```java
  DataReport.getInstance().init(DataReportInner.getInstance(), context,Configuration.builder() //进行一些设置
  .build())
```

> H5
```javascript
Dawn.init({
    ... // 其他参数
    reportLogs: ({ logs }) => {
        // 发送 http 请求或通过客户端协议上报 logs
    },
});
```

### 设置节点 oid (Object ID)

- 启动SDK后，需要将目标元素设置上合适的oid，oid的类型分为2种：`page` 和 `element`
- 这取决于BI对节点如何定义，一般来说某个独立的 `XXViewController`建议配置为 `xx_page`的页面节点类型
- 而 `按钮、UI组件`等适合设置为 `xx_btn` `xx_cell`的element节点。

但是每个页面的**顶层节点**必须被设置为**page节点**，并且它默认情况下会自动成为**根节点**

> ***这里涉及了多个关键名词，比如oid, page节点, 根节点等，相关解释在 [关键概念](https://eventtracing.github.io/docs/About/Keyworks), [以及文档](https://eventtracing.github.io/docs/QuickStart/iOS#%E8%AE%BE%E7%BD%AE%E8%8A%82%E7%82%B9-oid)***


**设置 page 节点**

> 可以给 UIViewController 设置 page 节点，等价于给 vc.view 设置

> iOS

```objc
/* The following two methods are equivalent */
// Set page node for vc
[EventTracingBuilder viewController:self pageId:@"page_list"];
// set page node for view
[EventTracingBuilder view:vc. view pageId:@"page_list"];
```
> Android
```java
NodeBuilder.getNodeBuilder(Activity).setPageId("pageId")
```

> H5
```javascript
export default () => {
  return (
    <div
      data-log={JSON.stringify({
        oid: 'page_web_test',
        isPage: true,
        events: ['_pv', '_pd'],
      })}
    >
    </div>
  );
};
```

**设置 element 节点**

> iOS
```objc
// Set the view as an element node
[[EventTracingBuilder view:self.tableView elementId:@"auto_impress_test_list"] build:^(id<EventTracingLogNodeBuilder> _Nonnull builder) {
     builder
         // Exposure start, exposure end, click, etc. will be automatically checked
         .buildinEventLogDisableStrategy(ETNodeBuildinEventLogDisableStrategyNone)
         // Set an object parameter, all buried points generated by the object will carry this parameter
         .params.set(@"auto_key", @"auto_val_123");
}];
```

> Android
```java
NodeBuilder.getNodeBuilder(view).setElementId("elementId")
            .setVisibleMargin(10, -10, 0, 0)                        
            .setReportPolicy(ReportPolicy.REPORT_POLICY_EXPOSURE)   
            .params()                                               
            .putBIPosition(2)                                       
            .putBITitle("xxx")                                      
            .putBICustomParam("xxx", "xxx")
```

> H5
```javascript
export default () => {
  return (
    <div
      data-log={JSON.stringify({
        oid: 'btn_web_test',
        events: ['_ev', '_ec'],
      })}
    >
    </div>
  );
};
```

### 自动打点

**一些内置事件列表**

支持的自动打点事件包括:

- **曝光**：默认开启，分为页面曝光(`_pv`)和元素曝光(`_ev`)
- **点击**：默认开启，元素被点击 `_ec`
- **结束曝光**：默认关闭，页面曝光结束(`_pd`)和元素曝光结束(`_ed`)
- **冷启动**：默认开启，`_ac`
- **进入前台**：默认开启，`_ai`
- **进入后台**：默认开启，`_ao`
- **滚动**：默认关闭，列表视图滚动 `_es`

**手动打点**

以上事件即支持自动打点，也支持手动触发打点，比如下方代码演示了如何手动触发1次 点击事件 `_ec`

> iOS
```objc
[EventTracingBuilder logWithView:view event:^(id<EventTracingLogNodeEventActionBuilder>  _Nonnull builder) {
    builder.ec();
}];
```

> Android
```java
  DataReporter.clickBI()
            .setTarget(view)
            .setParam("xx", "xx")
            .report()
```

> H5
```javascript
window.NE_DAWN.trigger(target, options);
```

### 可视化调试工具

- 为了更方便地进行本地埋点调试，我们开发了专门的埋点可视化调试工具
- 工具的相关用法见文档 [iOS](https://eventtracing.github.io/docs/iOS/debug_tools), [Android](https://eventtracing.github.io/docs/Android/debug_tools)

> 比如 iOS 可视化调试工具的截图

![image](https://user-images.githubusercontent.com/121547934/217413196-0e1141ae-f5d0-4ea6-beaf-051c2b01d248.png)

### 埋点实时校验工具

- 为了更方便地进行本地埋点校验，我们跟平台一起对接，做了埋点实时校验工具
- 工具的相关用法见文档 [iOS](https://eventtracing.github.io/docs/iOS/debug_tools), [Android](https://eventtracing.github.io/docs/Android/debug_tools)

## 开发者共建

欢迎广大开发者一起来添砖加瓦！下面是一些方式来更好的一起参与共建：

- **提Bugs，以及发现新需求**，你可以提 [issue](https://github.com/eventtracing/dawn/issues)
- **开发者贡献**：如果你有兴趣一起参与共建，可以先看下 以及开发者宣言 [code of conduct](https://github.com/eventtracing/dawn/blob/master/CODE_OF_CONDUCT.md) 以及 [开发者建议](https://eventtracing.github.io/docs/Contributing/intro)

## 一起探讨

你可以通过 [Discussions](https://github.com/eventtracing/dawn/discussions) 跟我们一起讨论

也可以加入到我们的 [slack工作区](https://join.slack.com/t/dawn-sva3699/shared_invite/zt-1r42giro6-lWTTfbRAqpwsvYthYDRC3A)

## License
了解更多参见 [LICENSE](./LICENSE)
