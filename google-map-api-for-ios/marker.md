# Marker



##### Make a standard marker

```swift
 let marker = GMSMarker()
        marker.position = CLLocationCoordinate2D(latitude: -33.86, longitude: 151.20)
        marker.title = "Sydney"
        marker.snippet = "Australia"
        marker.map = mapView

```

##### 

##### Change marker color

```swift
marker.icon = GMSMarker.markerImage(with: .black)
```



##### Custom marker icon

```swift
let position = CLLocationCoordinate2D(latitude:51.5, longitude: -0.127)
let london = GMSMarker(position: position)
london.title = "London"
london.icon = UIImage(named: "house")
london.map = mapView
```



##### Custom marker iconView

!FILENAME ViewController.swift

```swift
...
var london:GMSMarker?
var londonView:UIImageView?
...  
viewDidLoad(){
    let house = UIImage(named:"House")!.withRenderingMode(.alwaysTemplate)
    let markerView = UIImageView(image: house)
    markerView.tintColor = .red
    londonView = markerView
    
    let position = CLLocationCoordinate2D(latitude:51.5, longitude: -0.127)
    let marker = GMSMarker(position: position)
    marker.title = "London"
    marker.iconView = markerView
    marker.tracksViewChanges = true
    marker.map = mapView
    london = marker   
}

// 每次滑动地图，或者地图中心有变化时，标出地图中心的位置
func mapView(_ mapView:GMSMapView, idleAt position:GMSCameraPosition) {
    UIView.animate(withDuration:5.0, animations: { () -> Void in
      self.londonView?.tintColor = .blue
      }, completion: {(finished) in
        // Stop tracking view changes to allow CPU to idle.
        self.london?.tracksViewChanges = false
    })
  }
```

使用`iconView`时，请注意以下几点：

* 在`tracksViewChanges`设为`YES`时，`UIView`可能会请求资源，这会导致电池消耗增加。 相比之下，单帧`UIImage`为静态，并且不需要重新渲染。

* 如果您的屏幕上有很多标记，每个标记都有自己的`UIView`，并且所有标记都在同时跟踪更改，某些设备在渲染地图时可能会比较吃力。

* `iconView`不会响应用户交互，因为它只是一张视图快照。

* 无论`clipsToBounds`的实际值为何，视图都展现前者设为`YES`时的行为。 您可以应用作用于边界之外的变换，但是您绘制的对象必须位于对象的边界内。 所有变换/转换都会得到监视并加以应用。 简言之，子视图必须包含在视图中。

要确定何时设置`tracksViewChanges`属性，您应权衡性能注意事项与让标记自动重绘的优势。

例如：

* 如果您要进行一系列更改，则可以先将属性设为`YES`，然后再改回`NO`。

* 如果某个动画正在运行或者内容正在异步加载，您应将属性一直设为`YES`，直至操作完成。

  


