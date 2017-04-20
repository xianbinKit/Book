# Quick Start

follow : [https://developers.google.com/maps/documentation/ios-sdk/start](https://developers.google.com/maps/documentation/ios-sdk/start)

### RESUME

##### Install with CocoaPods

```
pod 'GoogleMaps'
pod 'GooglePlaces'
```

##### Integrate in Project

按以下步骤向`AppDelegate.swift`添加 API 密钥：

1. 添加以下 import 语句：
   ```
   import GoogleMaps
   import GooglePlaces  // if you use
   ```
2. 向您的`application(_:didFinishLaunchingWithOptions:)`方法添加以下内容，使用您的API KEY替代_YOUR\_API\_KEY_：
   ```
   GMSServices.provideAPIKey("YOUR_API_KEY")
   ```
3. 如果您也使用 Places API，请按下图所示再次添加密钥：
   ```
   GMSPlacesClient.provideAPIKey("YOUR_API_KEY")
   ```



从 iOS 9 和 Xcode 7 开始，应用必须通过在`Info.plist`文件中指定架构来声明其打算打开的网址架构。 当用户点击地图上的 Google 徽标时，Google Maps SDK for iOS 会打开 Google 地图移动应用，因此您的应用需要声明相关的网址架构。

要声明 Google Maps SDK for iOS 所使用的 URL 架构，请将以下几行代码添加到您的`Info.plist`中：

```
<key>LSApplicationQueriesSchemes</key>
    <array>
        <string>googlechromes</string>
        <string>comgooglemaps</string>
    </array>
```

  


