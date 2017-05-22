# Firebase Analytics

[https://firebase.google.com/docs/analytics/ios/start](https://firebase.google.com/docs/analytics/ios/start)

##### LogEvent

用于发送用户的各种动作，比如打开app,  登录，购买，假如许愿单，完成教程，通关等等。

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

##### Automatically collected events 自动记录的事件

[https://support.google.com/firebase/answer/6317485](https://support.google.com/firebase/answer/6317485)



##### Custom Event

```swift
FIRAnalytics.logEventWithName("share_image", parameters: [
  "name": name,
  "full_text": text
  ])
```

Custom Event will not show in Firebase dashboard, but you can filter to find them, and they also transfer to BigQuery.



