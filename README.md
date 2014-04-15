AppStore SDK接入指南
==============
这个指南给你接入sdk做引导
一、sdk接入流程说明


1、把LKSDK工程文件导入Xcode工程，添加StoreKit.framework

2、在AppDelegate.h 导入LKSDK.h /LKUncaughtExceptionHandler.h头文件

3、在AppDelegate.m 入口函数-(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 调用  以下三个函数

  （1）开启崩溃日志搜集处理
InstallUncaughtExceptionHandler();

（2）设置调试模式，可以开启打印日志模式
		 [LKSDK defaultSDK].isDebug = YES ;
			该值设为NO，则关闭打印日志模式 默认值为NO

（3）支付sdk进行初始化
  [[LKSDK defaultSDK] LKInitWithAppId:@"40" AndAppKey:@"" AndServerid:@"" AndExtStr:@"cqzj.linekong.t0#cqzj.linekong.t1#cqzj.linekong.t2#cqzj.linekong.t3#cqzj.linekong.t4#cqzj.linekong.t5" AndInterfaceOrientation:LKInterfaceOrientationMaskLandscape AndInitFinishCallbackBlock:^(NSString *str) {
        NSLog(@"%@",str);
    }];

4、在购买商店的类导入LKSDK.h头文件，点击购买按钮时调用

  [[LKSDK defaultSDK] LKPaymentWithOrderId:@"" AndAmount:@"cqzj.linekong.t0" AndCustomInfo:@"mjs521cy" AndRoleId:@"" AndZoneId:@"" AndCallBackURL:@"http://api.x.union.8864.com/mps/apple/charging.php" AndGateWayId:@"40014" AndExtStr:@"" AndPayFinishCallBack:^(BOOL code, NSString *str) {
        if (code == YES) {
         NSLog(@"%@",str);
        }
    }];
实际参数以分配给厂商的为准


二、sdk  API接口说明

1、设置调试模式，可以开启打印日志模式
		 [LKSDK defaultSDK].isDebug = YES ;
			该值设为NO，则关闭打印日志模式

		2、初始化接口
		（1）不含有block回调的接口，这个接口会在未来某一天废除		
	-(void)LKInitWithAppId:(NSString*)appId AndAppKey:(NSString*)appKey AndServerid:(NSString*)serverid AndExtStr:(NSString *)extStr;

			参数说明

			appId 为游戏id ，从蓝港平台组申请

			appKey 传为@“”空字符串

			serverid 传为@“”空字符串

			extStr  传入产品列表信息 如：@“cqzj.linekong.t0#cqzj.linekong.t1#cqzj.linekong.t2#cqzj.linekong.t3#cqzj.linekong.t4#cqzj.linekong.t5”，各产品之间以# 分割

		3、支付接口

（1）不含有block回调的接口，这个接口会在未来某一天废除-(void)LKPaymentWithOrderId:(NSString*)orderId AndAmount:(NSString*)amount AndCustomInfo:(NSString*)customInfo  AndRoleId:(NSString*)roleId AndZoneId:(NSString*)zoneId  AndCallBackURL:(NSString *)callBackURL AndGateWayId:(NSString*)gateWayId;

		       参数说明
			orderId 传@“”

			amount 传购买产品的id

			customInfo 传玩家的名字

                        roleId 可以传@“”	

                        zoneId 可以传@“”

                        callBackURL 传入回调地址

                         gateWayId  传入网关id
