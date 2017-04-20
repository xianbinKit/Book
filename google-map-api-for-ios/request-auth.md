# Request Auth for iOS location





\#FILENAME ViewControoler.swift

```swift
...
var locationManager = CLLocationManager()
...
func requestAuth(){
        // first time enter app
        if CLLocationManager.authorizationStatus() == .notDetermined {
            locationManager.requestWhenInUseAuthorization()
        }
        // refuse already
        else if CLLocationManager.authorizationStatus() == .denied {
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
        else if CLLocationManager.authorizationStatus() == .authorizedWhenInUse {
            //... do what you want ...//
        }

    }

```



