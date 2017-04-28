# ios Swift Gyroscope 陀螺仪 详解

##### Start

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    motionManager = CMMotionManager()
    ...
}

func startGyroscopeUpdates() {
        // Check whether the gyroscope is available
        guard self.motionManager.isGyroAvailable else { return }
        if self.motionManager.isGyroAvailable {
            // Update the recurring update interval
            let updateInterval = 0.2
            self.motionManager.gyroUpdateInterval = updateInterval
            // Start gyroscope updates
            self.motionManager.startGyroUpdates(to: OperationQueue.main) {
                // if not update UI elements for ex: self.view, delete [weak self]
                [weak self] (gyroData, error) in
                // Handle error
                if let e = error {
                    print(e.localizedDescription)
                }
                // Handler to process gyroscope data
                if let rotation = gyroData?.rotationRate{
                    // Handle rotation
                    print(String(format: "Rotation In X : %.2f", rotation.x))
                    print(String(format: "Rotation In Y : %.2f", rotation.y))
                    print(String(format: "Rotation In Z : %.2f", rotation.z))
                }

            }
        }
    }
```

##### Stop

```swift
func stopUpdates() {
    // Check whether the gyroscope is actived
    if self.motionManager.isGyroActive {
        // stop gyroscope updates
        self.motionManager.stopGyroUpdates()
    }
}
```

## Gyroscope 数据

数据形式和Acceleration一样，具体请看 [Acceleration](/core-motion/acceleration.md) .

