# KVO的例子

##### 添加 

```swift
// map view observer for updating current position
        mapView.addObserver(self,
                            forKeyPath: "myLocation",
                            options: NSKeyValueObservingOptions.new,
                            context: nil)
```

被观察者：mapView 添加一个观察者\(addObserver\).  
观察者：self \(当前viewControler或者其他Object\).  
被观察的值\(keyPath\): myLocation \(被观察者的值，MapView.myLocation\).  
要观察的属性:NSKeyValueObservingOptions.new,有新值，旧值等等.

##### 通知\(回调\)

```swift
override func observeValue(forKeyPath keyPath: String?, of object: Any?, change: [NSKeyValueChangeKey : Any]?, context: UnsafeMutableRawPointer?) {
        if keyPath == "myLocation" {
            if !firstLocationUpdate{
                if let change = change{
                    let location : CLLocation = change[NSKeyValueChangeKey.newKey] as! CLLocation
                    self.mapView.camera = GMSCameraPosition.camera(withTarget: location.coordinate, zoom: 14)
                    firstLocationUpdate = true
                    print("pisition updated")
```

当被观察者\(mapView\)的值\(myLocation\)改变时，会调用观察者\(self\)的函数.  
观察选项将放入一个字典change里.

