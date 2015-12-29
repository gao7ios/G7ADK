# G7ADK

[![CocoaPods](https://img.shields.io/cocoapods/v/FLEX.svg)](http://cocoapods.org/?q=G7ADK)
 [![CocoaPods](https://img.shields.io/cocoapods/l/FLEX.svg)](https://github.com/gao7ios/G7ADK/blob/master/LICENSE)
 [![CocoaPods](https://img.shields.io/cocoapods/p/FLEX.svg)]()
 [![Weibo: @yumous](https://img.shields.io/badge/contact-@aboutios-blue.svg?style=flat)](http://weibo.com/aboutios)

搞趣网iOS客户端广告SDK，对接第三方平台的广告，包括横幅广告，插屏广告，开屏广告。

## 最少代码接入最多平台

- 线程自动执行，根据广告后台配置展示平台广告，自动上报展示和点击；
- 支持的广告平台：广点通、百度移动、Inmobi、Admob、Gao7(自家);
- 支持的广告类型：横幅广告、插屏广告、开屏广告；

  AD	| GDT | InMobi |     BaiduMob   | Admob | Gao7 |
-------	| --- | ------ |     --------   | ----- | ---- |
横幅    	|  √  |   √    |    √           |       |  √   |
插屏    	|  √  |   √    |    √           |  √    |  √   |
开屏    	|  √  |   √    |    √ (No Rec.) |  √    |  √   |




## 如何使用


**需要:**

- 操作系统: Mac OS X 10.10.3 及以上版本 
- 开发工具: Xcode 7.0 及以上版本 
- 支持设备: iPhone/iPod Touch/iPad (iOS 7.0 及以上版本)

**依赖:**

- G7Core.framework 1.1.2.20151223
- G7BLL.framework 1.2.3.151224
- G7Network.framework
- GoogleMobileAds.framework 7.6.0
- SystemConfiguration.framework
- Foundation.framework
- ZipArchive.framework
- AdSupport.framework
- CoreLocation.framework
- QuarzCore.framework
- CoreTelephony.framework
- Security.framework
- StoreKit.framework
- Social.framework
- MessageUI.framework
- MediaPlayer.framework
- EventKit.framework
- EventKitUI.framework
- CoreFoundation.framework
- CoreLocation.framework
- CoreTelephony.framework
- CFNetwork.framework
- AVFoundation.framework
- AudioToolbox.framework
- AdSupport.framework
- libc++.dylib 或 libc++.tbd
- libsqlite3.0.dylib 或 libsqlite3.0.tbd
- libz.dylib 或 libz.tbd


**项目修改**

- Other Linker Flags 添加 -lstdc++    -ObjC

**注意事项**

- 目前广告平台都是用HTTP请求，支持iOS9需要在 info.plist 文件中增加 
如下配置:(信任 HTTP 请求)

```
	<dict>
		<key>NSAllowsArbitraryLoads</key>
		<true/>
	</dict>
```


**接入**

- Banner

```objc
	
	//创建Banner广告，PlaceId由后台配置
	id<IADKUnionAdView> adview = [[ADKUnion sharedInstance] addBannerViewWithFrame:CGRectMake(0, 0, self.view.width, 50) placeId:1];
	[self.view addSubview:(UIView *)adview];
	
	//设置 IADKUnionAdBannerDelegate
	[[ADKUnion sharedInstance] forwardingAdBannerDelegateTo:self];
	
```


- 插屏

```objc
	
	//开启插屏广告，默认开启
		[[ADKUnion sharedInstance] setEnableAdInterstitial:YES];
	
	//设置 IADKUnionAdInterstitialDelegate
	[[ADKUnion sharedInstance] forwardingAdInterstitialDelegateTo:self];
	
```

- 开屏


```objc
	
	//开启开屏广告，默认开启
		[[ADKUnion sharedInstance] setEnableSplashAd:YES];
	
	//设置开屏广告背景颜色，当图片格式不符合屏幕尺寸时，SDK会按比例压缩图片大小，使其适应；
		[[ADKUnion sharedInstance] setSplashBackgroundColor:[UIColor whiteColor]];
		
	//设置 IADKUnionAdSplashDelegate
	[[ADKUnion sharedInstance] forwardingAdSplashDelegateTo:self];
	
```

- 其他

```objc

	//开启Debug模式，SDK会打印所有广告日志
	[[ADKUnion sharedInstance] setDebugMode:YES];
	
	//暂停广告执行，只对当前广告周期有效
	[[ADKUnion sharedInstance] pause];
	
	//继续之前暂停的广告线程，只对当前广告周期有效
	[[ADKUnion sharedInstance] resume];
	
	/**
 	* <p>*停止广告执行</p>
	* <p>该方法会停止当前所有广告线程，并取消广告展示</p>
	* <p>在下一次的广告周期(即应用重启或间隔30分钟从后台启动)，广告线程会自动重新开始执行</p>
 	*/
	[[ADKUnion sharedInstance] stop];
	
	//移除广告
	[[ADKUnion sharedInstance] removeAdViewWithId:AdID];
	
```


## TODO
- 开放Debug模式
- 优化自家开屏广告线程
