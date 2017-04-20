# Current Position

最新版本的google map sdk并不需要使用LocationManager去读取当前地址，只需要将 `mapView.isMyLocationEnabled` 设置为 `true`。

!FILENAME ViewController.swift

```swift
...
func ViewDidLoad(){
        ...
        // update current position after UI init
        DispatchQueue.main.async {
                print("dispatch in viewdidload")
                self.mapView.isMyLocationEnabled = true
        }
        ...
        // map view observer for updating current position
        mapView.addObserver(self,
                            forKeyPath: "myLocation",
                            options: NSKeyValueObservingOptions.new,
                            context: nil)
}

...
// listen to myLocation keypath value changes
override func observeValue(forKeyPath keyPath: String?, of object: Any?, change: [NSKeyValueChangeKey : Any]?, context: UnsafeMutableRawPointer?) {
        if keyPath == "myLocation" {
            // print("update")
            if !firstLocationUpdate{
                if let change = change{
                    let location : CLLocation = change[NSKeyValueChangeKey.newKey] as! CLLocation
                    self.mapView.camera = GMSCameraPosition.camera(withTarget: location.coordinate, zoom: 14)
                    self.mapView.isHidden = false
                    firstLocationUpdate = true
                    // when false, we can't see current position in map, so the solution is remove observer. or use flag as firstLocationUpdate
                    //                    self.mapView.isMyLocationEnabled = false
                    print("position updated")
                }
            }
        }
        
}
 ...
```



##### Update current location use LocationManager

!FILENAME ViewController.swift

```swift
...
var locationManager = CLLocationManager()
...
func viewDidLoad(){
    ...
    locationManager = CLLocationManager()
    locationManager.desiredAccuracy = kCLLocationAccuracyBest
    locationManager.requestAlwaysAuthorization()
    locationManager.distanceFilter = 50
    locationManager.startUpdatingLocation()
    locationManager.delegate = self
    ...
}

extension ViewController: CLLocationManagerDelegate {
  ...
  // Handle incoming location events.
  func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
    let location: CLLocation = locations.last!
    print("Location: \(location)")

    let camera = GMSCameraPosition.camera(withLatitude: location.coordinate.latitude,
                                          longitude: location.coordinate.longitude,
                                          zoom: zoomLevel)

    if mapView.isHidden {
      mapView.isHidden = false
      mapView.camera = camera
    } else {
      mapView.animate(to: camera)
    }

    listLikelyPlaces()
  }

  // Handle location manager errors.
  func locationManager(_ manager: CLLocationManager, didFailWithError error: Error) {
    locationManager.stopUpdatingLocation()
    print("Error: \(error)")
  }
}
```



