# iOS Swift device orientation 获取





```swift
func addDeviceOrientationObserver(){
        if !UIDevice.current.isGeneratingDeviceOrientationNotifications{
            UIDevice.current.beginGeneratingDeviceOrientationNotifications()
        }
        NotificationCenter.default.addObserver(
            self,
            selector:  #selector(deviceDidRotate),
            name: .UIDeviceOrientationDidChange,
            object: nil
        )
}

func deviceDidRotate() {
        if UIDevice.current.orientation == previousDeviceOrientation { return }
        previousDeviceOrientation = UIDevice.current.orientation
        print("deviceDidRotate",previousDeviceOrientation.rawValue)
}
```





