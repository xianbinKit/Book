# Firebase Analytics

[https://firebase.google.com/docs/analytics/ios/start](https://firebase.google.com/docs/analytics/ios/start)

### LogEvent

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



