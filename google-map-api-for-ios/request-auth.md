# Request Auth for iOS location

!FILENAME ViewControoler.swift

```swift
...
var locationManager = CLLocationManager()
...

func viewDidLoad(){
...
locationManager.delegate = self
...
}

func requestAuth(){
        // first time enter app
        if CLLocationManager.authorizationStatus() == .notDetermined {
            locationManager.requestWhenInUseAuthorization()
        }
        // refuse already
        else if CLLocationManager.authorizationStatus() == .denied {
           requestAuthAlert()            
        }
        else if CLLocationManager.authorizationStatus() == .authorizedWhenInUse {
            //... do what you want ...//
        }
}

func requestAuthAlert(){
  let alertController = UIAlertController(
                title: "location auth refuse",
                message:
                "if you want to unlock auth, pleas go to...(TODO, jump to auth automaticallly)",
                preferredStyle: .alert)
            let okAction = UIAlertAction(
                title: "ok", style: .default, handler:nil)
            alertController.addAction(okAction)
            self.present(alertController, animated:true, completion: nil)

}

// out of ViewController Class
extension MapViewController: CLLocationManagerDelegate {
  // Handle authorization for the location manager.
  func locationManager(_ manager: CLLocationManager, didChangeAuthorization status: CLAuthorizationStatus) {
    switch status {
    case .restricted:
      print("Location access was restricted.")
    case .denied:
      print("User denied access to location.")
      // Display the map using the default location.
      mapView.isHidden = false
      // or show Alert
      requestAuthAlert()
    case .notDetermined:
      print("Location status not determined.")
    case .authorizedAlways: fallthrough
    case .authorizedWhenInUse:
      print("Location status is OK.")
    }
  }

  // Handle location manager errors.
  func locationManager(_ manager: CLLocationManager, didFailWithError error: Error) {
    locationManager.stopUpdatingLocation()
    print("Error: \(error)")
  }
}
```



