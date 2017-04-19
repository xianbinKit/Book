# CocoaPods 简明

##### In your project root

```
cd <YOUR_PROJECT_ROOT_PATH>
```

##### Init

```
pod init
```

##### Edit

```
nano PodFile
```

 在文件的最上方你会看到下面的内容，建议设定platform, 不然会只兼容最新版本的iOS.  
use\_frameworks在iOS 8以上兼容，会把第三方库编译成framework的形式，加快程序编译。如果没有这一行，将会是源文件的形式。

> > \# Uncomment this line to define a global platform for your project  
> > platform :ios, '9.0'  
> > \# Uncomment this line if you're using Swift  
> > use\_frameworks

##### Install

```
pod install
```

##### Update repo

有时候找不到对的库，无法安装，有可能是local repo没有更新。

```
pod repo update
```

这个过程没有任何提示，repo有时候会很大。可以尝试删除，重新安装，就有进度条显示了

```
pod repo remove master
pod setup
```



