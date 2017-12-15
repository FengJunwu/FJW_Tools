# FJW_Tools
学习中的一些经验总结
#pragma mark ============== 禁止手机睡眠 ============
/*
 [UIApplication sharedApplication].idleTimerDisabled = YES;
 */

#pragma mark ============== 隐藏某行cell ============

//未验证成功

/*
 - (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath
 {
 // 如果是你需要隐藏的那一行，返回高度为0
 if(indexPath.row == YouWantToHideRow)
 return 0;
 return 44;
 }
 
 // 然后再你需要隐藏cell的时候调用
 [self.tableView beginUpdates];
 [self.tableView endUpdates];

 */
#pragma mark ============== 禁用button高亮 ============
/*
 button.adjustsImageWhenHighlighted = NO;
 或者在创建的时候
 UIButton *button = [UIButton buttonWithType:UIButtonTypeCustom];
 */

#pragma mark ============== tableview遇到这种报错failed to obtain a cell from its dataSource ============
/*
 是因为你的cell被调用的早了。先循环使用了cell，后又创建cell。顺序错了
 可能原因：1、xib的cell没有注册 2、内存中已经有这个cell的缓存了(也就是说通过你的cellId找到的cell并不是你想要的类型)，这时候需要改下cell的标识
 */

#pragma mark ============== cocoa pods报这个错误：unable to access 'https://github.com/facebook/pop.git/': Operation timed out after 0 milliseconds with 0 out of 0 bytes received ============

/*
 解决办法：原因可能是网络问题，网络请求超时了，只需要重试就行了
 */

#pragma mark ============== cocoa pods 出现ERROR: While executing gem ... (Errno::EPERM) ============
/*
 解决办法：
 
 https://segmentfault.com/q/1010000002926243
 */

#pragma mark ============== 动画切换window的根控制器 ============

/*
 // options是动画选项
 
 [UIView transitionWithView:[UIApplication sharedApplication].keyWindow duration:0.5f options:UIViewAnimationOptionTransitionCrossDissolve animations:^{
 
 BOOL oldState = [UIView areAnimationsEnabled];
 
 [UIView setAnimationsEnabled:NO];
 
 [UIApplication sharedApplication].keyWindow.rootViewController = [RootViewController new];
 
 [UIView setAnimationsEnabled:oldState];
 
 } completion:^(BOOL finished) {
 
 
 }];
 */

#pragma mark ============== 去除数组中重复的对象 ============

/*
 NSArray *newArr = [oldArr valueForKeyPath:@"@distinctUnionOfObjects.self"];
 */
#pragma mark ============== 编译的时候遇到 no such file or directory: ／users／apple／XXX ============

/*
 是因为编译的时候，在此路径下找不到这个文件，解决这个问题，首先是是要检查缺少的文件是不是在工程中，如果不在工程中，需要从本地拖进去，如果发现已经存在工程中了，或者拖进去还是报错，这时候需要去build phases中搜索这个文件，这时候很可能会搜出现两个相同的文件，这时候，有一个路径是正确的，删除另外一个即可。如果删除了还是不行，需要把两个都删掉，然后重新往工程里拖进这个文件即可http://mmbiz.qpic.cn/mmbiz_png/foPACGrddJ3GTXzxIGTKF1dhXOIyvP7nJdqicZhdkNa8fa1Ic5zwXDLnFzGxnDnrdUYNKiauo3YIcBOv6xM5TxwQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1
 */

#pragma mark ============== iOS8系统中，tableView最好实现下-tableView: heightForRowAtIndexPath:这个代理方法，要不然在iOS8中可能就会出现显示不全或者无法响应事件的问题 ============

#pragma mark ============== iOS8中实现侧滑功能的时候这个方法必须实现，要不然在iOS8中无法侧滑 ============
/*
 // 必须写的方法，和editActionsForRowAtIndexPath配对使用，里面什么不写也行
 
 - (void)tableView:(UITableView *)tableView commitEditingStyle:(UITableViewCellEditingStyle)editingStyle forRowAtIndexPath:(NSIndexPath *)indexPath {

 }
 */

#pragma mark ============== 三个通知--时间 ============
/*
 NSSystemTimeZoneDidChangeNotification监听修改时间界面的两个按钮状态变化
 UIApplicationSignificantTimeChangeNotification 监听用户改变时间 （只要点击自动设置按钮就会调用） 
 NSSystemClockDidChangeNotification 监听用户修改时间（时间不同才会调用）
 */

#pragma mark ============== SDWebImage本地缓存有时候会害人。如果之前缓存过一张图片，即使下次服务器换了这张图片，但是图片url没换，用sdwebimage下载下来的还是以前那张,所以遇到这种问题，不要先去怼服务器，清空下缓存再试就好了。 ============

#pragma mark ============== 上线前注意 ============
/*
 1）、删掉代码中所有的测试代码
 2）、如果后台有审核模式，提醒后台开启此模式
 3）、主流程再跑一跑
 4）、全局搜索waring，检查所有标记waring的地方
 */

#pragma mark ============== 给一个view截图 ============
/*
 UIGraphicsBeginImageContextWithOptions(view.bounds.size, YES, 0.0);
 
 [view.layer renderInContext:UIGraphicsGetCurrentContext()];
 
 UIImage *img = UIGraphicsGetImageFromCurrentImageContext();
 
 UIGraphicsEndImageContext();
 */

#pragma mark ============== 开发中如果要动态修改tableView的tableHeaderView或者tableFooterView的高度，需要给tableView重新设置，而不是直接更改高度。正确的做法是重新设置一下tableView.tableFooterView = 更改过高度的view。为什么？其实在iOS8以上直接改高度是没有问题的，在iOS8中出现了contentSize不准确的问题，这是解决办法。============

#pragma mark ============== collectionView的内容小于其宽高的时候是不能滚动的，设置可以滚动 ============
/*
 collectionView.alwaysBounceHorizontal = YES;
 collectionView.alwaysBounceVertical = YES;
 */

#pragma mark ============== 设置navigationBar上的title颜色和大小 ============
/*
  [self.navigationController.navigationBar setTitleTextAttributes:@{NSForegroundColorAttributeName : [UIColor youColor], NSFontAttributeName : [UIFont systemFontOfSize:15]}]
 */

#pragma mark ============== 颜色转图片 ============

/*
 
 + (UIImage *)cl_imageWithColor:(UIColor *)color {
 CGRect rect = CGRectMake(0.0f, 0.0f, 1.0f, 1.0f);
 UIGraphicsBeginImageContext(rect.size);
 CGContextRef context = UIGraphicsGetCurrentContext();
 CGContextSetFillColorWithColor(context, [color CGColor]);
 CGContextFillRect(context, rect);
 UIImage *image = UIGraphicsGetImageFromCurrentImageContext();
 UIGraphicsEndImageContext();
 return image;
 
 }
 
 */

#pragma mark ============== 强／弱引用 ============
/*
 #define WeakSelf(type)  __weak typeof(type) weak##type = type; // weak
 #define StrongSelf(type)  __strong typeof(type) type = weak##type; // strong
 */


#pragma mark ============== 由角度转换弧度 ============
/*
 #define DegreesToRadian(x) (M_PI * (x) / 180.0)
 */

#pragma mark ============== 由弧度转换角度 ============
/*
 #define RadianToDegrees(radian) (radian*180.0)/(M_PI)
 */

#pragma mark ============== 获取图片资源 ============
/*
 #define GetImage(imageName) [UIImage imageNamed:[NSString stringWithFormat:@"%@",imageName]]
 */

#pragma mark ============== 获取temp ============

/*
 #define PathTemp NSTemporaryDirectory()
 */

#pragma mark ============== 获取沙盒 Document ============

/*
 #define PathDocument [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) firstObject]
 */

#pragma mark ============== 获取沙盒 Cache ============

/*
 #define PathCache [NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES) firstObject]
 */

#pragma mark ============== GCD代码只执行一次 ============

/*
 #define kDISPATCH_ONCE_BLOCK(onceBlock) static dispatch_once_t onceToken; dispatch_once(&onceToken, onceBlock);
 实现：
 kDISPATCH_ONCE_BLOCK(^{
 
 });
 */

#pragma mark ============== 自定义NSLog ============

/*
 #ifdef DEBUG
 
 #define NSLog(fmt, ...) NSLog((@"%s [Line %d] " fmt), __PRETTY_FUNCTION__, __LINE__, ##__VA_ARGS__)
 
 #else
 
 #define NSLog(...)
 
 #endif
 */

#pragma mark ============== Font ============

/*
 #define FontL(s)             [UIFont systemFontOfSize:s weight:UIFontWeightLight]
 
 #define FontR(s)             [UIFont systemFontOfSize:s weight:UIFontWeightRegular]
 
 #define FontB(s)             [UIFont systemFontOfSize:s weight:UIFontWeightBold]
 
 #define FontT(s)             [UIFont systemFontOfSize:s weight:UIFontWeightThin]
 
 #define Font(s)              FontL(s)
 */

#pragma mark ============== FORMAT ============

/*
 #define FORMAT(f, ...)      [NSString stringWithFormat:f, ## __VA_ARGS__]
 */

#pragma mark ============== 在主线程上运行 ============

/*
 #define kDISPATCH_MAIN_THREAD(mainQueueBlock) dispatch_async(dispatch_get_main_queue(), mainQueueBlock);
 实现：
 kDISPATCH_MAIN_THREAD(^{
 
 });
 */
#pragma mark ============== 开启异步线程 ============

/*
 #define ge(globalQueueBlock) dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), globalQueueBlocl);
 */

#pragma mark ============== 通知 ============

/*
 #define NOTIF_ADD(n, f)     [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(f) name:n object:nil]
 
 #define NOTIF_POST(n, o)    [[NSNotificationCenter defaultCenter] postNotificationName:n object:o]
 
 #define NOTIF_REMV()        [[NSNotificationCenter defaultCenter] removeObserver:self]
 */

#pragma mark ============== 随机颜色 ============
/*
 + (UIColor *)RandomColor {
 
 NSInteger aRedValue = arc4random() % 255;
 
 NSInteger aGreenValue = arc4random() % 255;
 
 NSInteger aBlueValue = arc4random() % 255;
 
 UIColor *randColor = [UIColor colorWithRed:aRedValue / 255.0f green:aGreenValue / 255.0f blue:aBlueValue / 255.0f alpha:1.0f];
 
 return randColor;
 
 }
 */

#pragma mark ============== 获取window ============

/*
 +(UIWindow*)getWindow {
 
 UIWindow* win = nil; //[UIApplication sharedApplication].keyWindow;
 
 for (id item in [UIApplication sharedApplication].windows) {
 
 if ([item class] == [UIWindow class]) {
 
 if (!((UIWindow*)item).hidden) {
 
 win = item;
 
 break;
 
 }
 
 }
 
 }
 
 return win;
 
 }
 */

#pragma mark ============== 修改textField的placeholder的字体颜色、大小 ============
/*
 [textField setValue:[UIColor redColor] forKeyPath:@"_placeholderLabel.textColor"];
 
 [textField setValue:[UIFont boldSystemFontOfSize:16] forKeyPath:@"_placeholderLabel.font"];
 */

#pragma mark ============== 统一收起键盘 ============
/*
 [[[UIApplication sharedApplication] keyWindow] endEditing:YES];
 */

#pragma mark ============== 控制屏幕旋转，在控制器中写 ============

/*
 
 * 是否支持自动转屏 

- (BOOL)shouldAutorotate {
    
    return YES;
    
}


* 支持哪些屏幕方向 

- (UIInterfaceOrientationMask)supportedInterfaceOrientations {
    
    return UIInterfaceOrientationMaskLandscapeLeft | UIInterfaceOrientationMaskLandscapeRight;
    
}


* 默认的屏幕方向（当前ViewController必须是通过模态出来的UIViewController（模态带导航的无效）方式展现出来的，才会调用这个方法） 

- (UIInterfaceOrientation)preferredInterfaceOrientationForPresentation {
    
    return UIInterfaceOrientationLandscapeLeft | UIInterfaceOrientationLandscapeRight;
    
}
 */


#pragma mark ============== 获取app缓存大小 ============

/**
 - (CGFloat)getCachSize {
 
 
 NSUInteger imageCacheSize = [[SDImageCache sharedImageCache] getSize];
 
 //获取自定义缓存大小
 
 //用枚举器遍历 一个文件夹的内容
 
 //1.获取 文件夹枚举器
 
 NSString *myCachePath = [NSHomeDirectory() stringByAppendingPathComponent:@"Library/Caches"];
 
 NSDirectoryEnumerator *enumerator = [[NSFileManager defaultManager] enumeratorAtPath:myCachePath];
 
 __block NSUInteger count = 0;
 
 //2.遍历
 
 for (NSString *fileName in enumerator) {
 
 NSString *path = [myCachePath stringByAppendingPathComponent:fileName];
 
 NSDictionary *fileDict = [[NSFileManager defaultManager] attributesOfItemAtPath:path error:nil];
 
 count += fileDict.fileSize;//自定义所有缓存大小
 
 }
 
 // 得到是字节  转化为M
 
 CGFloat totalSize = ((CGFloat)imageCacheSize+count)/1024/1024;
 
 return totalSize;
 
 }
 */

#pragma mark ============== 清理app缓存 ============
/*
 - (void)handleClearView {
 
 //删除两部分
 
 //1.删除 sd 图片缓存
 
 //先清除内存中的图片缓存
 
 [[SDImageCache sharedImageCache] clearMemory];
 
 //清除磁盘的缓存
 
 [[SDImageCache sharedImageCache] clearDisk];
 
 //2.删除自己缓存
 
 NSString *myCachePath = [NSHomeDirectory() stringByAppendingPathComponent:@"Library/Caches"];
 
 [[NSFileManager defaultManager] removeItemAtPath:myCachePath error:nil];
 
 }
 */

#pragma mark ============== 交换两个方法实现 ============

/*
 Class aClass = [self class];
 
 SEL originalSelector = @selector(viewWillAppear:);
 
 SEL swizzledSelector = @selector(xxx_viewWillAppear:);
 
 Method originalMethod = class_getInstanceMethod(aClass, originalSelector);
 
 Method swizzledMethod = class_getInstanceMethod(aClass, swizzledSelector);
 
 
 BOOL didAddMethod = class_addMethod(aClass,
 
 originalSelector,
 
 method_getImplementation(swizzledMethod),
 
 method_getTypeEncoding(swizzledMethod));
 
 
 if (didAddMethod) {
 
 class_replaceMethod(aClass,
 
 swizzledSelector,
 
 method_getImplementation(originalMethod),
 
 method_getTypeEncoding(originalMethod));
 
 } else {
 
 method_exchangeImplementations(originalMethod, swizzledMethod);
 
 }

 */

#pragma mark ============== 打印百分号和引号 ============
/*
 NSLog(@"%%");
 
 NSLog(@"\"");
 */

#pragma mark ============== 几个常用权限判断 ============
/*
 #import <CoreLocation/CoreLocation.h>
 
 if ([CLLocationManager authorizationStatus] ==kCLAuthorizationStatusDenied) {
 
 NSLog(@"没有定位权限");
 
 }
 
 #import <AVFoundation/AVCaptureDevice.h>
 #import <AVFoundation/AVMediaFormat.h>
 AVAuthorizationStatus statusVideo = [AVCaptureDevice authorizationStatusForMediaType:AVMediaTypeVideo];
 
 if (statusVideo == AVAuthorizationStatusDenied) {
 
 NSLog(@"没有摄像头权限");
 
 }
 
 //是否有麦克风权限
 
 AVAuthorizationStatus statusAudio = [AVCaptureDevice authorizationStatusForMediaType:AVMediaTypeAudio];
 
 if (statusAudio == AVAuthorizationStatusDenied) {
 
 NSLog(@"没有录音权限");
 
 }
 
 #import <Photos/Photos.h>
 [PHPhotoLibrary requestAuthorization:^(PHAuthorizationStatus status) {
 
 if (status == PHAuthorizationStatusDenied) {
 
 NSLog(@"没有相册权限");
 
 }
 
 }];
 */

#pragma mark ============== 获取手机型号 ============
/*
 #import "sys/utsname.h"
 
 + (NSString *)getDeviceInfo {
 
 struct utsname systemInfo;
 
 uname(&systemInfo);
 
 NSString *platform = [NSString stringWithCString:systemInfo.machine encoding:NSASCIIStringEncoding];
 
 if ([platform isEqualToString:@"iPhone1,1"]) return @"iPhone 2G";
 
 if ([platform isEqualToString:@"iPhone1,2"]) return @"iPhone 3G";
 
 if ([platform isEqualToString:@"iPhone2,1"]) return @"iPhone 3GS";
 
 if ([platform isEqualToString:@"iPhone3,1"]) return @"iPhone 4";
 
 if ([platform isEqualToString:@"iPhone3,2"]) return @"iPhone 4";
 
 if ([platform isEqualToString:@"iPhone3,3"]) return @"iPhone 4";
 
 if ([platform isEqualToString:@"iPhone4,1"]) return @"iPhone 4S";
 
 if ([platform isEqualToString:@"iPhone5,1"]) return @"iPhone 5";
 
 if ([platform isEqualToString:@"iPhone5,2"]) return @"iPhone 5";
 
 if ([platform isEqualToString:@"iPhone5,3"]) return @"iPhone 5c";
 
 if ([platform isEqualToString:@"iPhone5,4"]) return @"iPhone 5c";
 
 if ([platform isEqualToString:@"iPhone6,1"]) return @"iPhone 5s";
 
 if ([platform isEqualToString:@"iPhone6,2"]) return @"iPhone 5s";
 
 if ([platform isEqualToString:@"iPhone7,1"]) return @"iPhone 6 Plus";
 
 if ([platform isEqualToString:@"iPhone7,2"]) return @"iPhone 6";
 
 if ([platform isEqualToString:@"iPhone8,1"]) return @"iPhone 6s";
 
 if ([platform isEqualToString:@"iPhone8,2"]) return @"iPhone 6s Plus";
 
 // 日行两款手机型号均为日本独占，可能使用索尼FeliCa支付方案而不是苹果支付
 
 if ([platform isEqualToString:@"iPhone9,1"])    return @"国行、日版、港行iPhone 7";
 
 if ([platform isEqualToString:@"iPhone9,2"])    return @"港行、国行iPhone 7 Plus";
 
 if ([platform isEqualToString:@"iPhone9,3"])    return @"美版、台版iPhone 7";
 
 if ([platform isEqualToString:@"iPhone9,4"])    return @"美版、台版iPhone 7 Plus";
 
 if ([platform isEqualToString:@"iPhone8,4"]) return @"iPhone SE";
 
 if ([platform isEqualToString:@"iPod1,1"]) return @"iPod Touch 1G";
 
 if ([platform isEqualToString:@"iPod2,1"]) return @"iPod Touch 2G";
 
 if ([platform isEqualToString:@"iPod3,1"]) return @"iPod Touch 3G";
 
 if ([platform isEqualToString:@"iPod4,1"]) return @"iPod Touch 4G";
 
 if ([platform isEqualToString:@"iPod5,1"]) return @"iPod Touch 5G";
 
 if ([platform isEqualToString:@"iPad1,1"]) return @"iPad 1G";
 
 if ([platform isEqualToString:@"iPad2,1"]) return @"iPad 2";
 
 if ([platform isEqualToString:@"iPad2,2"]) return @"iPad 2";
 
 if ([platform isEqualToString:@"iPad2,3"]) return @"iPad 2";
 
 if ([platform isEqualToString:@"iPad2,4"]) return @"iPad 2";
 
 if ([platform isEqualToString:@"iPad2,5"]) return @"iPad Mini 1G";
 
 if ([platform isEqualToString:@"iPad2,6"]) return @"iPad Mini 1G";
 
 if ([platform isEqualToString:@"iPad2,7"]) return @"iPad Mini 1G";
 
 if ([platform isEqualToString:@"iPad3,1"]) return @"iPad 3";
 
 if ([platform isEqualToString:@"iPad3,2"]) return @"iPad 3";
 
 if ([platform isEqualToString:@"iPad3,3"]) return @"iPad 3";
 
 if ([platform isEqualToString:@"iPad3,4"]) return @"iPad 4";
 
 if ([platform isEqualToString:@"iPad3,5"]) return @"iPad 4";
 
 if ([platform isEqualToString:@"iPad3,6"]) return @"iPad 4";
 
 if ([platform isEqualToString:@"iPad4,1"]) return @"iPad Air";
 
 if ([platform isEqualToString:@"iPad4,2"]) return @"iPad Air";
 
 if ([platform isEqualToString:@"iPad4,3"]) return @"iPad Air";
 
 if ([platform isEqualToString:@"iPad4,4"]) return @"iPad Mini 2G";
 
 if ([platform isEqualToString:@"iPad4,5"]) return @"iPad Mini 2G";
 
 if ([platform isEqualToString:@"iPad4,6"]) return @"iPad Mini 2G";
 
 if ([platform isEqualToString:@"i386"]) return @"iPhone Simulator";
 
 if ([platform isEqualToString:@"x86_64"]) return @"iPhone Simulator";
 
 return platform;
 
 }
 */

#pragma mark ============== 长按复制功能 ============

/*
 - (void)viewDidLoad
 
 {
 
 [self.view addGestureRecognizer:[[UILongPressGestureRecognizer alloc] initWithTarget:self action:@selector(pasteBoard:)]];
 
 }
 
 - (void)pasteBoard:(UILongPressGestureRecognizer *)longPress {
 
 if (longPress.state == UIGestureRecognizerStateBegan) {
 
 UIPasteboard *pasteboard = [UIPasteboard generalPasteboard];
 
 pasteboard.string = @"需要复制的文本";
 
 }
 
 }
 */

#pragma mark ============== 设置启动页后，依然显示之前的 ============
/*
 删除app，手机重启，重新安装
 */

#pragma mark ============== 判断图片类型 ============
/*
 //通过图片Data数据第一个字节 来获取图片扩展名
 
 - (NSString *)contentTypeForImageData:(NSData *)data
 
 {
 
 uint8_t c;
 
 [data getBytes:&c length:1];
 
 switch (c)
 
 {
 
 case 0xFF:
 
 return @"jpeg";
 
 
 case 0x89:
 
 return @"png";
 
 
 case 0x47:
 
 return @"gif";
 
 
 case 0x49:
 
 case 0x4D:
 
 return @"tiff";
 
 
 case 0x52:
 
 if ([data length] < 12) {
 
 return nil;
 
 }
 
 
 NSString *testString = [[NSString alloc] initWithData:[data subdataWithRange:NSMakeRange(0, 12)] encoding:NSASCIIStringEncoding];
 
 if ([testString hasPrefix:@"RIFF"]
 
 && [testString hasSuffix:@"WEBP"])
 
 {
 
 return @"webp";
 
 }
 
 
 return nil;
 
 }
 
 
 return nil;
 
 }
 */
#pragma mark ============== 获取手机和app信息 ============
/*
 NSDictionary *infoDictionary = [[NSBundle mainBundle] infoDictionary];
 
 CFShow(infoDictionary);
 
 // app名称
 
 NSString *app_Name = [infoDictionary objectForKey:@"CFBundleDisplayName"];
 
 // app版本
 
 NSString *app_Version = [infoDictionary objectForKey:@"CFBundleShortVersionString"];
 
 // app build版本
 
 NSString *app_build = [infoDictionary objectForKey:@"CFBundleVersion"];
 
 
 
 
 //手机序列号
 
 NSString* identifierNumber = [[UIDevice currentDevice] uniqueIdentifier];
 
 NSLog(@"手机序列号: %@",identifierNumber);
 
 //手机别名： 用户定义的名称
 
 NSString* userPhoneName = [[UIDevice currentDevice] name];
 
 NSLog(@"手机别名: %@", userPhoneName);
 
 //设备名称
 
 NSString* deviceName = [[UIDevice currentDevice] systemName];
 
 NSLog(@"设备名称: %@",deviceName );
 
 //手机系统版本
 
 NSString* phoneVersion = [[UIDevice currentDevice] systemVersion];
 
 NSLog(@"手机系统版本: %@", phoneVersion);
 
 //手机型号
 
 NSString* phoneModel = [[UIDevice currentDevice] model];
 
 NSLog(@"手机型号: %@",phoneModel );
 
 //地方型号  （国际化区域名称）
 
 NSString* localPhoneModel = [[UIDevice currentDevice] localizedModel];
 
 NSLog(@"国际化区域名称: %@",localPhoneModel );
 
 
 NSDictionary *infoDictionary = [[NSBundle mainBundle] infoDictionary];
 
 // 当前应用名称
 
 NSString *appCurName = [infoDictionary objectForKey:@"CFBundleDisplayName"];
 
 NSLog(@"当前应用名称：%@",appCurName);
 
 // 当前应用软件版本  比如：1.0.1
 
 NSString *appCurVersion = [infoDictionary objectForKey:@"CFBundleShortVersionString"];
 
 NSLog(@"当前应用软件版本:%@",appCurVersion);
 
 // 当前应用版本号码   int类型
 
 NSString *appCurVersionNum = [infoDictionary objectForKey:@"CFBundleVersion"];
 
 NSLog(@"当前应用版本号码：%@",appCurVersionNum);
 */

#pragma mark ============== 获取一个类的所有属性 ============
/*
 id LenderClass = objc_getClass("Lender");
 
 unsigned int outCount, i;
 
 objc_property_t *properties = class_copyPropertyList(LenderClass, &outCount);
 
 for (i = 0; i < outCount; i++) {
 
 objc_property_t property = properties[i];
 
 fprintf(stdout, "%s %s\n", property_getName(property), property_getAttributes(property));
 
 }
 */


#pragma mark ============== image圆角 ============

/*
 - (UIImage *)circleImage{
 
 // NO代表透明
 
 UIGraphicsBeginImageContextWithOptions(self.size, NO, 1);
 
 // 获得上下文
 
 CGContextRef ctx = UIGraphicsGetCurrentContext();
 
 // 添加一个圆
 
 CGRect rect = CGRectMake(0, 0, self.size.width, self.size.height);
 
 // 方形变圆形
 
 CGContextAddEllipseInRect(ctx, rect);
 
 // 裁剪
 
 CGContextClip(ctx);
 
 // 将图片画上去
 
 [self drawInRect:rect];
 
 UIImage *image = UIGraphicsGetImageFromCurrentImageContext();
 
 UIGraphicsEndImageContext();
 
 return image;
 
 }
 */

#pragma mark ============== image拉伸 ============
/*
 + (UIImage *)resizableImage:(NSString *)imageName
 
 {
 
 UIImage *image = [UIImage imageNamed:imageName];
 
 CGFloat imageW = image.size.width;
 
 CGFloat imageH = image.size.height;
 
 return [image resizableImageWithCapInsets:UIEdgeInsetsMake(imageH * 0.5, imageW * 0.5, imageH * 0.5, imageW * 0.5) resizingMode:UIImageResizingModeStretch];
 
 }
 */

#pragma mark ============== JSON字符串转字典 ============

/*
 + (NSDictionary *)parseJSONStringToNSDictionary:(NSString *)JSONString {
 
 NSData *JSONData = [JSONString dataUsingEncoding:NSUTF8StringEncoding];
 
 NSDictionary *responseJSON = [NSJSONSerialization JSONObjectWithData:JSONData options:NSJSONReadingMutableLeaves error:nil];
 
 return responseJSON;
 
 }
 */
#pragma mark ============== 身份证号验证 ============
/*
- (BOOL)validateIdentityCard {
    
    BOOL flag;
    
    if (self.length <= 0) {
        
        flag = NO;
        
        return flag;
        
    }
    
    NSString *regex2 = @"^(\\d{14}|\\d{17})(\\d|[xX])$";
    
    NSPredicate *identityCardPredicate = [NSPredicate predicateWithFormat:@"SELF MATCHES %@",regex2];
    
    return [identityCardPredicate evaluateWithObject:self];
    
}
 */

#pragma mark ============== 导入自定义字体库 ============
/*
 1、找到你想用的字体的 ttf 格式，拖入工程
 
 2、在工程的plist中增加一行数组，“Fonts provided by application”
 
 3、为这个key添加一个item，value为你刚才导入的ttf文件名
 
 4、直接使用即可：label.font = [UIFont fontWithName:@"你刚才导入的ttf文件名" size:20.0]；
 */

#pragma mark ============== 拿到当前正在显示的控制器，不管是push进去的，还是present进去的都能拿到 ============

/*
 - (UIViewController *)getVisibleViewControllerFrom:(UIViewController*)vc {
 
 if ([vc isKindOfClass:[UINavigationController class]]) {
 
 return [self getVisibleViewControllerFrom:[((UINavigationController*) vc) visibleViewController]];
 
 }else if ([vc isKindOfClass:[UITabBarController class]]){
 
 return [self getVisibleViewControllerFrom:[((UITabBarController*) vc) selectedViewController]];
 
 } else {
 
 if (vc.presentedViewController) {
 
 return [self getVisibleViewControllerFrom:vc.presentedViewController];
 
 } else {
 
 return vc;
 
 }
 
 }
 
 }
 */

#pragma mark ============== runtime为一个类动态添加属性 ============
/*
 // 动态添加属性的本质是: 让对象的某个属性与值产生关联
 
 objc_setAssociatedObject(self, WZBPlaceholderViewKey, placeholderView, OBJC_ASSOCIATION_RETAIN_NONATOMIC);
 */

#pragma mark ============== 获取runtime为一个类动态添加的属性 ============
/*
 objc_getAssociatedObject(self, WZBPlaceholderViewKey);
 */

#pragma mark ============== KVO监听某个对象的属性 ============

/*
 // 添加监听者
 
 [self addObserver:self forKeyPath:property options:NSKeyValueObservingOptionNew context:nil];
 
 
 // 当监听的属性值变化的时候会来到这个方法
 
 - (void)observeValueForKeyPath:(NSString *)keyPath ofObject:(id)object change:(NSDictionary *)change context:(void *)context {
 
 if ([keyPath isEqualToString:@"property"]) {
 
 [self textViewTextChange];
 
 } else {
 
 }
 
 }
 */

#pragma mark ============== Reachability判断网络状态 ============

/*
 NetworkStatus status = [[Reachability reachabilityForInternetConnection] currentReachabilityStatus];
 
 if (status == NotReachable) {
 
 NSLog(@"当前设备无网络");
 
 }
 
 if (status == ReachableViaWiFi) {
 
 NSLog(@"当前wifi网络");
 
 }
 
 if (status == NotReachable) {
 
 NSLog(@"当前蜂窝移动网络");
 
 }
 */
