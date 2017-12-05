# cordova-plugin-ionic-umeng

Umeng统计SDK更新至：
```
Android v6.1.2, iOS v4.2.4
```

## 集成友盟

```
cordova plugins add https://github.com/open-more/cordova-plugin-ionic-umeng.git

```

### android集成
修改自己的APPKEY
在PROJECT_ROOT/platforms/android/AndroidManifest.xml里修改自己的友盟APPKEY：
```
<meta-data android:name="UMENG_APPKEY" android:value="YOUR_APP_KEY" />
```

在PROJECT_ROOT/platforms/android/src/[YOUR_PACKAGE_NAME]/MainActivity.java里添加：

```
/**
 * onCreate中调用
 */
private void initUmengSDK() 
{
    com.umeng.analytics.MobclickAgent.setScenarioType(this, com.umeng.analytics.MobclickAgent.EScenarioType.E_UM_NORMAL);
    com.umeng.analytics.MobclickAgent.setDebugMode(true);
    com.umeng.analytics.MobclickAgent.openActivityDurationTrack(false);
    // MobclickAgent.setSessionContinueMillis(1000);
}

@Override
protected void onResume() {
    super.onResume();
    com.umeng.analytics.MobclickAgent.onResume(this);
}

@Override
protected void onPause() {
   super.onPause();
   com.umeng.analytics.MobclickAgent.onPause(this);
}
```

### ios集成
在PROJECT_ROOT/platforms/ios/[YOUR_APP_NAME]]/Classes/AppDelegate.m里导入头文件
```
#import <UMMobClick/MobClick.h>
```
在didFinishLaunchingWithOptions方法返回语句前添加：
```
UMConfigInstance.appKey = @"YOUR_APP_KEY";
UMConfigInstance.channelId = @"AppStore";
[MobClick startWithConfigure:UMConfigInstance];
```

