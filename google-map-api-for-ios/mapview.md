# MapView 创建

##### Create mapview in viewDidLoad\(\)

!FILENAME ViewController.swift

```swift
...
// A default location to use when location permission is not granted.
let defaultLocation = CLLocation(latitude: -33.869405, longitude: 151.199)

override func viewDidLoad() {
        super.viewDidLoad()
        // camera
        let camera = GMSCameraPosition.camera(withLatitude: defaultLocation.coordinate.latitude,
                                              longitude: defaultLocation.coordinate.longitude,
                                              zoom: zoomLevel)
        // map view
        let mapView = GMSMapView.map(withFrame: self.view.frame, camera: camera)
        mapView.delegate = self
        //mapView.mapType = .satellite
        self.mapView = mapView

        // map view observer for updating current position
        mapView.addObserver(self,
                            forKeyPath: "myLocation",
                            options: NSKeyValueObservingOptions.new,
                            context: nil)

        let marker = GMSMarker()
        marker.position = CLLocationCoordinate2D(latitude: -33.86, longitude: 151.20)
        marker.title = "Sydney"
        marker.snippet = "Australia"
        marker.map = mapView
        mapView.isMyLocationEnabled = true
        // Ask for My Location data after the map has already been added to the UI. before that, no needs to update location
        DispatchQueue.main.async {
            print("dispatch in viewdidload")

        }
        view.addSubview(mapView)
        mapView.isHidden = true

        // GMSGeocoder use for find location information
        self.geocoder = GMSGeocoder()
    }
```



