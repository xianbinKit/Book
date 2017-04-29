# iOS swift Device Motion 详解

Core Motion里功能最强大的一部分，包含了 Acceleration 和 Gyroscope.

##### Start

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    motionManager = CMMotionManager()
    ...
}

func startDeviceMotionUpdates(){
        // Check whether the device motion is available
        guard self.motionManager.isDeviceMotionAvailable else { return }
        // Update the recurring update interval
        let updateInterval = 0.2
        self.motionManager.deviceMotionUpdateInterval = updateInterval
        // Start accelerometer updates
        self.motionManager.startDeviceMotionUpdates(to: OperationQueue.main) {
            // if not update UI elements for ex: self.view, delete [weak self]
            [weak self] (deviceMotionData, error) in
            // Handle error
            if let e = error {
                print(e.localizedDescription)
            }
            // Handle user acceleration
            if let userAcceleration = deviceMotionData?.userAcceleration{
                print(String(format: "userAcceleration In X : %.2f", userAcceleration.x))
                print(String(format: "userAcceleration In Y : %.2f", userAcceleration.y))
                print(String(format: "userAcceleration In Z : %.2f", userAcceleration.z))
            }
            // Handle gravity
            if let gravity = deviceMotionData?.gravity {
                print( String(format : "gravity In X : %.2f"   , gravity.x) )
                print( String(format : "gravity In Y : %.2f"   , gravity.y) )
                print( String(format : "gravity In Z : %.2f"   , gravity.z) )
            }
            // Handle attribute
            if let attitude = deviceMotionData?.attitude{
                // Handle rotation in Euler angles
                print(String(format : "attitude yaw   : %.2f"   , attitude.yaw))
                print(String(format : "attitude pitch : %.2f"   , attitude.pitch))
                print(String(format : "attitude roll  : %.2f"   , attitude.roll))
                // Handle rotation in quaternion
                print(String(format : "quaternion x     : %.2f"   , attitude.quaternion.x))
                print(String(format : "quaternion y     : %.2f"   , attitude.quaternion.y))
                print(String(format : "quaternion z     : %.2f"   , attitude.quaternion.z))
                print(String(format : "quaternion w     : %.2f"   , attitude.quaternion.w))
                // Handle rotation in Matrix
                print("rotation matrix : ",attitude.rotationMatrix)   // 3x3 matrix
            }
            // Handle rotation
            if let rotation = deviceMotionData?.rotationRate{
                print(String(format: "Rotation In X : %.2f", rotation.x))
                print(String(format: "Rotation In Y : %.2f", rotation.y))
                print(String(format: "Rotation In Z : %.2f", rotation.z))
            }
        }
    }
```

##### Stop

```swift
func stopUpdates() {
    // Check whether the device motion is actived
    if self.motionManager.isDeviceMotionActive {
    // stop device motion updates
    self.motionManager.stopDeviceMotionUpdates()
    }
}
```

## Device Motion 数据格式

##### userAcceleration

这个数据是acceleration 不包含重力的数据。数据是瞬时数据。

##### gravity

可以获取重力在xyz方向上的分量

##### attribute

attribute的数据是持久的，所有变化都相对于startUpdate 时的状态进行改变。

* yaw :  围绕Z轴旋转，逆时针为正，顺势正为负。值在\[-PI,+PI\]之间, 旋转-180度和旋转+180度是同一个位置。以startUpdate时刻手机的方向为0，之后数值的变化都相对于这个初始位置。

![](/assets/image_yaw.gif)

* roll : 围绕Y轴旋转，面向右转为正，反之为负。值在\[-PI,+PI\]之间, 旋转-180度和旋转+180度是同一个位置\(背面朝上的位置\)。 以平方手机，面朝上为初始0。

![](/assets/image_roll.gif)

* pitch :  围绕X轴旋转，面向自己旋转为正，反之为负。值在\[-Pi/2,+PI/2\]之间。以平方手机，面朝上为初始0。

![](/assets/image_pitch.gif)

在做pitch运动时，会改变yaw和roll的值，比如当手机直立前后pitch时，其实也做了yaw和roll运动，因为手机的面一会朝上，一会朝下。所以pitch的取值范围只有2 \* PI/2, 然后根据yaw和roll的值来做具体判断。

更多关于欧拉角（Euler angles）和四元数（Quaternion）请到 [这里](/core-motion/euler-angles-and-quaternion.md) 。

##### rotation

和Gyroscope得到的值一样。

## 更精准的测量

```swift
self.motionManager.startDeviceMotionUpdates(using: <#T##CMAttitudeReferenceFrame#>, 
to: <#T##OperationQueue#>, 
withHandler: <#T##CMDeviceMotionHandler##CMDeviceMotionHandler##(CMDeviceMotion?, Error?) -> Void#>)
```

这个函数允许赋予referenceFrame, 可以更加精准的测量，借助指南针修正误差，所有选项如下。

```swift
/*
 *  CMAttitudeReferenceFrame
 *  
 *  Discussion:
 *    CMAttitudeReferenceFrame indicates the reference frame from which all CMAttitude
 *        samples are referenced.
 *
 *    Definitions of each reference frame is as follows:
 *        - CMAttitudeReferenceFrameXArbitraryZVertical describes a reference frame in
 *          which the Z axis is vertical and the X axis points in an arbitrary direction
 *          in the horizontal plane.
 *        - CMAttitudeReferenceFrameXArbitraryCorrectedZVertical describes the same reference
 *          frame as CMAttitudeReferenceFrameXArbitraryZVertical with the following exception:
 *          when available and calibrated, the magnetometer will be used to correct for accumulated
 *          yaw errors. The downside of using this over CMAttitudeReferenceFrameXArbitraryZVertical
 *          is increased CPU usage.
 *        - CMAttitudeReferenceFrameXMagneticNorthZVertical describes a reference frame
 *          in which the Z axis is vertical and the X axis points toward magnetic north.
 *          Note that using this reference frame may require device movement to 
 *          calibrate the magnetometer.
 *        - CMAttitudeReferenceFrameXTrueNorthZVertical describes a reference frame in
 *          which the Z axis is vertical and the X axis points toward true north.
 *          Note that using this reference frame may require device movement to 
 *          calibrate the magnetometer.
 */
public struct CMAttitudeReferenceFrame : OptionSet {

    public init(rawValue: UInt)
    public static var xArbitraryZVertical: CMAttitudeReferenceFrame { get }
    public static var xArbitraryCorrectedZVertical: CMAttitudeReferenceFrame { get }
    public static var xMagneticNorthZVertical: CMAttitudeReferenceFrame { get }
    public static var xTrueNorthZVertical: CMAttitudeReferenceFrame { get }
}
```



