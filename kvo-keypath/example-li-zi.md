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

##### Context 的作用

 想象一下，假设有一个父类Person, 有两个子类Man和Woman如下。

```swift
Class Person {
    var age : Int
    override func observeValue(...){...}
}

class Man : Person {
    var hasWife : Bool
    override func observeValue(...){...}
}

class Woman : Person {
    var hasHusband : Bool
    override func observeValue(...){...}
}

var man : Man
var women : Woman
```

当我们对age进行监听的时候，希望Man类和Woman类分别处理自己的监听，可是age是在他们的公共父类Person里。那到底是谁的observeValue相应呢，可以给context一个数字Int，然后对context进行if判断。

