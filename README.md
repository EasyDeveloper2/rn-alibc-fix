
# rn-alibc-fix



## 注意点

|         版本        |   版本  |   文档  |
| :-----------------: | :---: | :---: |
| react-native < 0.60 | 3.0.2 | [点击](./README_0.5X.md) |


## 开始

`$ npm install rn-alibc-fix--save`

### iOS

打开`ios/Podfile`文件，添加以下（百川仓库）
```
require_relative '../node_modules/@react-native-community/cli-platform-ios/native_modules'
·······
source 'https://github.com/CocoaPods/Specs.git'
source 'http://repo.baichuan-ios.taobao.com/baichuanSDK/AliBCSpecs.git'

·······
target
```

### Android
打开`android/bulid.gradle`，添加以下仓库
```
······
allprojects {
    repositories {
        ·····
        maven {
            url "http://repo.baichuan-android.taobao.com/content/groups/BaichuanRepositories/"
        }
    }
}
······
```

### 其他配置


#### iOS

1. 把 `yw_1222.jpg` 拖入到项目中
2. `URL Schemes` 添加 `tbopen + 百川APPID` 
3. `LSApplicationQueriesSchemes` 添加 `tmall`、`tbopen`

#### Android

1. 复制百川安全图片 `yw_1222.jpg` 到 `android/app/src/main/res/drawable/yw_1222.jpg`


## 使用方法
详见examples目录


## 常见的问题

android 

{"code": "1", "message": "安全初始化失败"}

a.debug环境 请在百川获取安全图片时,使用app-debug.apk。
b.生产环境 请在使用app-release.apk获取。

如何还是报错 请将gradle 的版本 换成3.5.0以下(不含3.5.0) 我的是3.4.2 可以成功。

ios 初始化成功 授权不成功

请在appdelete.m文件添加下面代码

```
#import <AlibcTradeSDK/AlibcTradeSDK.h>

- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication annotation:(id)annotation
{
  if(![[AlibcTradeSDK sharedInstance]application:application openURL:url sourceApplication:sourceApplication annotation:annotation])
  {
    
  }
  return YES;
}

- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
{
  if(@available(iOS 9.0,*)){
    __unused BOOL isHandleByALBBSDK = [[AlibcTradeSDK sharedInstance] application:app openURL:url options:options];
  }else{
    
  }
  return YES;
}

```

