# // Check whether the accelerometer is available

```swift
        guard self.motionManager.isAccelerometerAvailable else { return }
        // Update the recurring update interval
        let updateInterval = 0.2
        self.motionManager.accelerometerUpdateInterval = updateInterval
        // Start accelerometer updates
Core Motion 详解
```

* Device Orientation
* Gyroscope
* Device Motion
* Accelerometer
* 欧拉角（Euler angles）和四元数（Quaternion）

Core Motion Manager 有两种获取数据的方式 **PULL** 和 **PUSH.  **因为PULL的方式比较简单，所以在这里举例简单说明一下，PUSH的方式将在后面的小节具体说明。

## PULL

##### Start

```swift
func startAccelerateUpdate(){
    // Check whether the accelerometer is available
    guard self.motionManager.isAccelerometerAvailable else { return }
    // Update the recurring update interval
    let updateInterval = 0.2
    self.motionManager.accelerometerUpdateInterval = updateInterval
    // Start accelerometer updates
    self.motionManager.startAccelerometerUpdates()    
}
```

在需要开启的地方调用这个方法，注意startAccelerometerUpdates\(\) 方法并不是立即起作用的，也就是说在这一行之后立即读取数据会得到nil.

##### Pull

```swift
func pullAccelerationData(){
    // check accelerometer is actived
    guard self.motionManager.isAccelerometerActive else { return }
    // Handler to process accelerometer data
    if let acceleration = accelerometerData?.acceleration{
        // Handle acceleration
        print(String(format: "Acceleration In X : %.2f", acceleration.x))
        print(String(format: "Acceleration In Y : %.2f", acceleration.y))
        print(String(format: "Acceleration In Z : %.2f", acceleration.z))
    }
}
```

##### Stop

```swift
func stopUpdates() {
    // Check whether the accelerometer is actived
    if self.motionManager.isAccelerometerActive {       
        // stop accelerometer updates
        self.motionManager.stopAccelerometerUpdates()   
    }
}
```

updateInterval 可以一个公用的变量，这样可以用到 acceleration 和gyroscope里，保持相同的更新频率。

 更新频率越快，耗电越快。

* 1/10    普通的view更新
* 1/60   游戏视频实时更新
* 更高的。。。



