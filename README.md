# Safe-Area

### 1.常用宏

正常获取导航栏高度和状态栏高度：

```
获取导航栏高度

self.navigationController.navigationBar.frame.size.height

获取状态栏高度：

UIApplication.sharedApplication.statusBarFrame.size.height
```

常用的宏定义：

```
#define  iPhoneX ([[UIScreen mainScreen] bounds].size.height==812)

#define kCustomSafeNavigationBarHeight (iPhoneX ? 88 : 64)//导航栏安全距离

#define kCustomSafeBottomHeight (iPhoneX ? 34 : 0)//底部安全距离

#define  kCustomSafeTopHeight      (iPhoneX ? 24.f : 0)

#define  kCustomSafeTabbarHeight         (iPhoneX ? (49.f+34.f) : 49.f)

// 底部宏  
#define SafeAreaBottomHeight (kScreenHeight == 812.0 ? 34 : 0)  

#define SafeAreaTopHeight (kScreenHeight == 812.0 ? 88 : 64)  
```

### 2.适配iPhone XS Max、iPhone XR

我们项目在获取机型等信息用的是DeviceKit这个第三方库，所以也需要更新一下才能获取到新机型的信息，最新版是1.8.1。在最新版有这样一个变量

```
    /// All Face ID Capable Devices
    static public var allFaceIDCapableDevices: [Device] {
      return [.iPhoneX, .iPhoneXs, .iPhoneXsMax, .iPhoneXr]
    }
```

由于iPhone X、iPhone XS、iPhone XS Max、iPhone XR这些机型的navigationBar高度以及tabBar高度都一致，所以可以用allFaceIDCapableDevices是否包含当前设备，来判断当前设备是否有“齐刘海”。

```
static let faceIDDeviceArray = Device.allFaceIDCapableDevices

static let navigationHeight: CGFloat = {
        if faceIDDeviceArray.contains(currentDevice) {
            return faceIDDeviceNavHeight
        } else {
            return ordinaryDeviceNavHeight
        }
    }()
```

同时DeviceKit中也提供这样一个方法，运行模拟器的时候调用，也会返回真实的设备名称

```
/// Get the real device from a device. If the device is a an iPhone8Plus simulator this function returns .iPhone8Plus (the real device).
    /// If the parameter is a real device, this function returns just that passed parameter.
    ///
    /// - parameter device: A device.
    ///
    /// - returns: the underlying device If the `device` is a `simulator`,
    /// otherwise return the `device`.
    public static func realDevice(from device: DeviceKit.Device) -> DeviceKit.Device
```

```
static let currentDevice = Device.realDevice(from: Device())
if currentDevice == .iPhoneX {}
// 取代以下写法
if Device() == .iPhoneX || Device() == .simulator(.iPhoneX) {}
```

最后别忘了再切两张启动图，因为iPhone XS和尺寸和iPhone X是一样的，所以iPhone XS可以忽略

iPhone XR：828px x 1792px

iPhone XS Max: 1242px x 2688px

