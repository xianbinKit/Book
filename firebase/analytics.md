# Firebase Analytics

[https://firebase.google.com/docs/analytics/ios/start](https://firebase.google.com/docs/analytics/ios/start)



### LogEvent

```swift
FIRAnalytics.logEvent(withName: kFIREventSelectContent, parameters: [
            kFIRParameterContentType:"cont" as NSObject,
            kFIRParameterItemID:"1" as NSObject
            ])
```

##### Event name : FIREEventNames.h

##### Parameter name : FIRParameterNames.h

Event和Parameter是相呼应的，具体请看FIREEventnames.h里的解释。



