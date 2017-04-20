# MapView 创建

##### Create mapview in viewDidLoad\(\)

!FILENAME ViewController.swift

```swift
...
// A default location to use when location permission is not granted.
let defaultLocation = CLLocation(latitude: -33.869405, longitude: 151.199)
// Greater value for zoom +
var zoomLevel: Float = 15.0

override func viewDidLoad() {
        super.viewDidLoad()
        // camera
        let camera = GMSCameraPosition.camera(withLatitude: defaultLocation.coordinate.latitude,
                                              longitude: defaultLocation.coordinate.longitude,
                                              zoom: zoomLevel)
        // map view
        let mapView = GMSMapView.map(withFrame: self.view.frame, camera: camera)
        // create a reference so we can use it easily
        self.mapView = mapView
        view.addSubview(mapView)
        // if we don't have permission to read current location, we can hide the mapView
        mapView.isHidden = true
    }
```

这个方法创建MapView的时候，好处是`mapView`是可以隐藏不显示的。当然这样的方法就是在`viewController`下面有两个View.一个`self.view`和一个`mapview`.  如果不想使用隐藏 `mapview` 的功能，可以做如下改变：

##### before

```swift
self.mapView = mapView
view.addSubView(mapView)
```

##### after

```swift
self.view = mapView
```

##### 

##### Create mapview in loadView

```swift
 override func loadView() {
     // Create a GMSCameraPosition that tells the map to display the
     // coordinate -33.86,151.20 at zoom level 6.
     let camera = GMSCameraPosition.camera(withLatitude: -33.86, longitude: 151.20, zoom: 6.0)
     let mapView = GMSMapView.map(withFrame: CGRect.zero, camera: camera)
     view = mapView
 }
```

这种方法和上面最后的改变一样，是替换了 `viewController`  的 `self.view`** **, 但是这个方法比上面的效率高，因为少创建了一个view.



