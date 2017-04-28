# ios Swift Acceleration 加速测量

##### Start

```swift
func startAccelerometerUpdates() {
        // Check whether the accelerometer is available
        if self.motionManager.isAccelerometerAvailable {
            // Update the recurring update interval
            let updateInterval = 0.2
            self.motionManager.accelerometerUpdateInterval = updateInterval
            // Start accelerometer updates
            self.motionManager.startAccelerometerUpdates(to: OperationQueue.main) {
                // if not update UI elements for ex: self.view, delete [weak self]
                [weak self] (accelerometerData, error) in
                // Handler to process accelerometer data
                if let acceleration = accelerometerData?.acceleration{
                    // Handle acceleration
                    print(String(format: "Acceleration In X : %.2f", acceleration.x))
                    print(String(format: "Acceleration In Y : %.2f", acceleration.y))
                    print(String(format: "Acceleration In Z : %.2f", acceleration.z))
                }

            }
        }
}
```

##### Stop

```swift
func stopUpdates() {
    // Check whether the accelerometer is actived
    if self.motionManager.accelerometerActive {       
        // stop accelerometer updates
        self.motionManager.stopAccelerometerUpdates()   
    }
}
```



## 加速计数据

![](/assets/img_acceleration_orientation.png)



由此方法得到的数据是包含了重力\(Gravity g ~= 0.98\)的，方向始终向下。可以用这个重力在xyz的分量来计算iPhone的倾斜。但是在 device Motion 章节有更好的方法。



