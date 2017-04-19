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



