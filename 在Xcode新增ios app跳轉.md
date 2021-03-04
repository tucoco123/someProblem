# 在Xcode新增ios app跳轉

註冊URL Scheme，即配置info.plist 檔案
```
<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Viewer</string>
			<key>CFBundleURLName</key>
			<string>com.varmeego.eatsoeasy</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>eatsoeasy</string>
			</array>
		</dict>
	</array>
```    
參考：https://www.jianshu.com/p/37a71cc24055

或是到target修改Info裡面修改URL Types
![](https://i.imgur.com/kv4s72h.png)


然後在info.plist 第三方登錄 添加URL Schemes白名單
```
<key>LSApplicationQueriesSchemes</key>
	<array>
		<string>https://eat-so-easy</string>
		<string>eatsoeasy://</string>
		<string>eatsoeasy</string>
	</array>
```
參考：https://www.jianshu.com/p/a1895c766400
    
在AppDelegate.m新增code

```
#import <React/RCTLinkingManager.h>
#pragma mark - Handling URLs
- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
  sourceApplication:(NSString *)sourceApplication annotation:(id)annotation
{
  return [RCTLinkingManager
           application:application openURL:url
           sourceApplication:sourceApplication
           annotation:annotation
         ];
}
```

參考：https://medium.com/@rossbulat/deep-linking-in-react-native-with-universal-links-and-url-schemes-7bc116e8ea8b


注意：專案名稱必須跟URL Scheme一樣，否則無法跳轉至該頁面

android＆ios可參考：https://www.itread01.com/content/1544675344.html