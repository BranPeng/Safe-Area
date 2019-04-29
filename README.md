# Safe-Area

获取导航栏高度

self.navigationController.navigationBar.frame.size.height

获取状态栏高度：

UIApplication.sharedApplication.statusBarFrame.size.height

常用的宏定义：

#define  iPhoneX ([[UIScreen mainScreen] bounds].size.height==812)

#define kCustomSafeNavigationBarHeight (iPhoneX ? 88 : 64)//导航栏安全距离

#define kCustomSafeBottomHeight (iPhoneX ? 34 : 0)//底部安全距离

#define  kCustomSafeTopHeight      (iPhoneX ? 24.f : 0)

#define  kCustomSafeTabbarHeight         (iPhoneX ? (49.f+34.f) : 49.f)

// 底部宏  
#define SafeAreaBottomHeight (kScreenHeight == 812.0 ? 34 : 0)  
#define SafeAreaTopHeight (kScreenHeight == 812.0 ? 88 : 64)  

