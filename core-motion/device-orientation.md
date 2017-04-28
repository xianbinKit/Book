# iOS Swift device orientation 获取

##### Start

```swift
func startDeviceOrientationObserver(){
        // the if check may not need because isGeneratingDeviceOrientationNotifications is true as default
        if !UIDevice.current.isGeneratingDeviceOrientationNotifications{
             // Turn on the accelerometer
            UIDevice.current.beginGeneratingDeviceOrientationNotifications()
        }
        // Register for orientation change notifications
        NotificationCenter.default.addObserver(
            self,
            selector:  #selector(deviceDidRotate),
            name: .UIDeviceOrientationDidChange,
            object: nil
        )
}

func deviceDidRotate() {
        // previousDeviceOrientation is an option
        if UIDevice.current.orientation == previousDeviceOrientation { return }
        // Respond to changes in orientation here
        previousDeviceOrientation = UIDevice.current.orientation
        print("deviceDidRotate",previousDeviceOrientation.rawValue)

}
```

虽然官方文档说，在开始检测device orientation和core motion manager之前，必须要调用 `UIDevice.current.beginGeneratingDeviceOrientationNotifications()` 但是在ios 10.3版本测试时，app启动后直接在 `viewDidLoad()` 中检测 `UIDevice.current.isGeneratingDeviceOrientationNotifications` 结果为 `true` , 说明默认已经是开启的. 并不需要调用begin...这个函数.

`startDeviceOrientationObserver()` 函数通常在需要时才启用，比如 `viewDidLoad()` .

在 `deviceDidRotate()` 函数里， 并不一定要检测前一个状态，目前只发现在程序启动时会出现当前方向等于前一个方向。

##### 

##### 所有方向的枚举

```swift
public enum UIDeviceOrientation : Int {    
    case unknown
    case portrait // Device oriented vertically, home button on the bottom
    case portraitUpsideDown // Device oriented vertically, home button on the top
    case landscapeLeft // Device oriented horizontally, home button on the right
    case landscapeRight // Device oriented horizontally, home button on the left
    case faceUp // Device oriented flat, face up
    case faceDown // Device oriented flat, face down
}
```

##### 

##### Stop

```swift
func stopOrientationObserver(){
        // Stop receiving orientation change notifications
        NotificationCenter.default.removeObserver(self)
        // Turn off the accelerometer
        UIDevice.current.endGeneratingDeviceOrientationNotifications()
}
```

`stopOrientationObserver()` 一般 `viewDidDisappear()` 里调用。  
在不需要时停用，可以节约电，比如在切换到一个不需要设备旋转的view时。

