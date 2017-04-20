# GMSMapViewDelegate



```swift
extension ViewController : GMSMapViewDelegate{
    func mapView(_ mapView:GMSMapView, didTapAt coordinate:CLLocationCoordinate2D) {
      print("You tapped at \(coordinate.latitude), \(coordinate.longitude)")
    }
}
```



