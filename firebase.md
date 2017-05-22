# Google Firebase

##### Install

* Install Firebase form Pod

```
pod 'Firebase'
```

* Download GoogleService-info.plist and add it into your project.

To download a config file for an iOS app:

1. Sign in to Firebase and open your project.
2. Click![](https://storage.googleapis.com/support-kms-prod/vMSwtm9y2uvHQAg2OfjmWpsBMtG4xwSIPWxh "the Settings icon")and select **Project settings**.
3. In the **Your apps **card, select the bundle ID of the app you need a config file for from the list.
4. Click![](https://lh3.googleusercontent.com/F_l_k73LFMmhZzlG3uUxR85785RlZFMYIszJFNl6Xq4k_xMLdgotg_O95JGyk8bSlQ=w24)**GoogleService-Info.plist**
   .

##### Import Firebase

* In your Application Delegate file

```swift
import Firebase
```

* In your `application:didFinishLaunchingWithOptions` method, create a Firebase shared instance.

```swift
FIRApp.configure()
```

| Pod availabale packages |
| :--- |


| Pod | Services |
| :--- | :--- |
| pod 'Firebase/Core' | Only Analytics |
| pod 'Firebase/AdMob' | AdMob |
| pod 'Firebase/Messaging' | Cloud Messaging / Notifications |
| pod 'Firebase/Database' | Realtime Database |
| pod 'Firebase/Invites' | Invites |
| pod 'Firebase/DynamicLinks' | Dynamic Links |
| pod 'Firebase/Crash' | Crash Reporting |
| pod 'Firebase/RemoteConfig' | Remote Config |
| pod 'Firebase/Auth' | Authentication |
| pod 'Firebase/AppIndexing' | App Indexing |
| pod 'Firebase/Storage' | Storage |



###  Debug 打印信息

Produst &gt; Scheme &gt; Edit scheme &gt; Run &gt; Arguments &gt; Arguments Passed On launch :

```
-FIRAnalyticsDebugEnabled
```



