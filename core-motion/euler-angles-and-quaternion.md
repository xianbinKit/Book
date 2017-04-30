# 欧拉角（Euler angles）和四元数（Quaternion）



## 欧拉角

欧拉角是表示朝向的最简方法，只需存储绕X、Y、Z轴旋转的角度，非常容易理解。你可以用vec3来存储一个欧拉角：

```
vec3 EulerAngles( RotationAroundXInRadians, RotationAroundYInRadians, RotationAroundZInRadians);
```

这三个旋转是依次施加的，通常的顺序是：Y-Z-X（但并非一定要按照这种顺序）。顺序不同，产生的结果也不同。

一个欧拉角的简单应用就是用于设置角色的朝向。通常，游戏角色不会绕X和Z轴旋转，仅仅绕竖直的Y轴旋转。因此，无需处理三个朝向，只需用一个float型变量表示方向即可。

另外一个使用欧拉角的例子是FPS相机：用一个角度表示头部朝向（绕Y轴），一个角度表示俯仰（绕X轴）。参见`common/controls.cpp`的示例。

不过，面对更加复杂的情况时，欧拉角就显得力不从心了。例如：

* 对两个朝向进行插值比较困难。简单地对X、Y、Z角度进行插值得到的结果不太理想。
* 实施多次旋转很复杂且不精确：必须计算出最终的旋转矩阵，然后据此推测书欧拉角。
* “臭名昭著”的“万向节死锁”\(Gimbal Lock\)问题有时会让旋转“卡死”。其他一些奇异状态还会导致模型方向翻转。
* 不同的角度可产生同样的旋转（例如-180°和180°）
* 容易出错——如上所述，一般的旋转顺序是YZX，如果用了非YZX顺序的库，就有麻烦了。
* 某些操作很复杂：如绕指定的轴旋转N角度。

四元数是表示旋转的好工具，可解决上述问题。



## 四元数

四元数由4个数\[x y z w\]构成，表示了如下的旋转：

```
//
 RotationAngle is in radians

x = RotationAxis.x * 
sin
(RotationAngle / 
2
)
y = RotationAxis.y * sin(RotationAngle / 
2
)
z = RotationAxis.z * sin(RotationAngle / 
2
)
w = cos(RotationAngle / 
2
)
```

`RotationAxis`，顾名思义即旋转轴。`RotationAngle`是旋转的角度。

![](/assets/img_Quaternion.png)



因此，四元数实际上存储了一个旋转轴和一个旋转角度。这让旋转的组合变简单了。





##### 解读四元数

四元数的形式当然不如欧拉角直观，不过还是能看懂的：xyz分量大致代表了各个轴上的旋转分量，而w=acos\(旋转角度/2\)。举个例子，假设你在调试器中看到了这样的值\[ 0.7 0 0 0.7 \]。x=0.7，比y、z的大，因此主要是在绕X轴旋转；而2\*acos\(0.7\) = 1.59弧度，所以旋转角度应该是90°。

同理，\[0 0 0 1\] \(w=1\)表示旋转角度 = 2_acos\(1\) = 0，因此这是一个_单位四元数\*（unit quaternion），表示没有旋转。



### Matrix

 最终的计算都是要换成Matrix计算的，因为mat计算很方便，欧拉角比较容易用于展示，但是不适合用于人的计算，而Mat比较适合机器计算。



