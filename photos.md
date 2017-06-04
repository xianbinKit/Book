# Photos

##### Save image to photo library

```
UIImageWriteToSavedPhotosAlbum(<#T##image: UIImage##UIImage#>, 
<#T##completionTarget: Any?##Any?#>, 
<#T##completionSelector: Selector?##Selector?#>, 
<#T##contextInfo: UnsafeMutableRawPointer?##UnsafeMutableRawPointer?#>)
```

##### Save video to photo library

```swift
PHPhotoLibrary.shared().performChanges({
    PHAssetChangeRequest.creationRequestForAssetFromVideo(atFileURL: self.output)
    }) { saved, error in
        if saved {
            let alertController = UIAlertController(title: "Your video was successfully saved", message: nil, preferredStyle: .alert)
            let defaultAction = UIAlertAction(title: "OK", style: .default, handler: nil)
            alertController.addAction(defaultAction)
            self.present(alertController, animated: true, completion: nil)
        }
}

```



