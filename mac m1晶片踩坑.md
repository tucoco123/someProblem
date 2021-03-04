# mac m1晶片踩坑

離職前一個禮拜公司買了新的mac mini，新的專案要開始了，主管要我幫忙設定環境，想說應該很快就弄完了，結果弄了兩天XD，簡單記錄一下過程。

一開始裝pod install一直卡卡卡，查半天一直以為是Xcode沒有設定arm64，仔細檢查後發現以前的開發團隊早就設定好了，尤其是Excluded Architectures=>Any ios Simulator SDK，怎麼查都是在講設定的文章，結果問題根本這些沒關係。

後來查到這篇文章[pod安装踩坑记录](https://www.jianshu.com/p/19094220ed2a)，原來是因為m1晶片不支援x86底下開發的package，尤其新的專案又是react native，要等到套件作者更新可能要一段時間，按照文章說的把會用到的應用程式改成使用Rosetta打開。

![](https://i.imgur.com/ayRVf4I.png)
![](https://i.imgur.com/IxUAcNZ.png)

建議這三個應用程式一定要打開，問題才會比較少。
1.	終端機 （在工具程式資料夾）
2.	Xcode
3.	Simulator（預設路徑：/Applications/Xcode.app/Contents/Developer/Applications/Simulator.app）

如果pod install還是裝不起來，可以試試用x86_64的pod install：

先安裝
```
sudo arch -x86_64 gem install ffi
```

再打指令
```
arch -x86_64 pod install
```

## 'Google-Maps-iOS-Utils/GMUKMLParser.h' file not

react-native-maps重新安裝完在Xcode build後，一定會出現這個bug

```
#import <Google_Maps_iOS_Utils/GMUKMLParser.h>
```

解決方法就是像上面的程式碼的'-改成_，再build一次就可以了。

以為解脫了，然後又出現了新的bug(昏倒) (´･_･`)
```
error message: duplicate symbols for architecture x86_64
```
簡單來說就是錯誤訊息裡提到的package引用了兩次，後來去react-native-maps github查看安裝流程文件，原本裝這個package時需要在Xcode目錄區參考AirgoogleMaps、AirMaps資料夾，於是我把這兩個從Xcode Delete references之後就沒有這個bug了。

猜測原因應該是React Native 60之後的版本都有 auto-link，因此不再需要手動增加參考路徑。

![](https://i.imgur.com/5lvav5J.png)


## build system
Xcode之後會拋棄舊式的compiler，更改設定在Xcode=>File=>Workspace Settings=>Build System 設定為『New Build System』


這些都設定完之後，在模擬器成功開啟ios app了(灑花)٩(^ᴗ^)۶

## Firebase/Core (~>7.6.0)

結果隔天母公司有人更新了package.json，把react-native-Firebase更新到了最新版，拉新code之後，pod install又裝不起來了，嗚嗚嗚 〒.〒 

錯誤訊息大概就是新套件要用到Firebase/Core 7.6.0，但是本地端cocoapods找不到，輸入pod update repo也不起作用，本來想說去 ~/.cocoapods/repos更新要用的套件就好了，結果打了指令還是不能更新...，最後是把[cocoapods整個移除重新安裝一次](https://stackoverflow.com/questions/43701352/what-exactly-does-pod-repo-update-do)，然後在podfile新增 pod 'Firebase/Core','7.6.0'，再一次pod install終於載到新版本的Firebase/Core，但是把這行從podfile移除掉又變不行裝...，明明本地端已經確定裝到最新版，照理說應該不用加這行也可以運行，反正我的任務只是要讓app跑得起來就好，其他就算了哈哈。