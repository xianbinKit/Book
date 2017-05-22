# Firebase Analytics

[https://firebase.google.com/docs/analytics/ios/start](https://firebase.google.com/docs/analytics/ios/start)

## Event

##### Automatically collected events 自动记录的事件

[https://support.google.com/firebase/answer/6317485](https://support.google.com/firebase/answer/6317485)

##### LogEvent

用于发送用户的各种动作，比如打开app,  登录，购买，假如许愿单，完成教程，通关等等。一共有200多种事件。

```swift
FIRAnalytics.logEvent(withName: kFIREventSelectContent, parameters: [
            kFIRParameterContentType:"cont" as NSObject,
            kFIRParameterItemID:"1" as NSObject
            ])
```

##### Event name : FIREEventNames.h

##### Parameter name : FIRParameterNames.h

Event和Parameter是相呼应的，具体请看FIREEventnames.h里的解释。

##### 

##### 

##### Custom Event

```swift
FIRAnalytics.logEventWithName("share_image", parameters: [
  "name": name,
  "full_text": text
  ])
```

Custom Event will not show in Firebase dashboard, but you can filter to find them, and they also transfer to BigQuery.

## User Property

用于收集用户数据，比如年龄层分段，地域，购买习惯等等。

##### 自动搜集的用户属性

[https://support.google.com/firebase/answer/6317486](https://support.google.com/firebase/answer/6317486)

注：仅当您的应用链接到[广告支持框架](https://developer.apple.com/library/ios/documentation/DeviceInformation/Reference/AdSupport_Framework/index.html)\(apple AdSupport\)时才会自动收集"年龄"、"性别"和"兴趣"属性。链接到此框架还会自动收集广告标识符 \(IDFA\)。



```swift
FIRAnalytics.setUserPropertyString(food, forName: "favorite_food")
```

注：注册此属性后，它将花几个小时的时间将收集的数据和该属性加入报告中。 当新数据可用时，可以将用户属性作为报告筛选器或目标设备定义。

