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

这个方法创建MapView的时候，好处是mapView是可以隐藏不显示的。当然这样的方法就是在viewController下面有两个View.一个\`self.view\`,

