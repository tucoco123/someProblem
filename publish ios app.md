Publish IOS
===
* [在 App Store Connect 查看您的App](#在-App-Store-Connect-查看您的App)
* [更改App資訊與提交審查](#更改App資訊與提交審查)
* [在Xcode打包上傳App](#在Xcode封裝上傳App)
* [[react native] ios app未正確linking packge](#react-native-ios-app未正確linking-packge)
* [TestFlight上做內部測試](#TestFlight上做內部測試)
* [Apple Store Connect 官方文件](https://help.apple.com/app-store-connect/#/)

# 在 App Store Connect 查看您的App

* 登入[App Store Connect](https://appstoreconnect.apple.com/)選取我的App，進入App選單，選擇您要發布的ios app
![](https://i.imgur.com/zphCRVD.png)

* 若還尚未建立App請點選App標題旁邊的+號新增『新的App』
建立App前請先至[apple developer](https://developer.apple.com/account/resources/identifiers)新增套件識別碼(Bundle ID)
可參考：[[官方文件]加入新的App](https://help.apple.com/app-store-connect/#/dev2cd126805)
![](https://i.imgur.com/YwCKCSR.png)
```
注意：Bundle ID必須是唯一的，若有人使用過Bundle ID將不能新增！(像app的身分證字號)
在使用Xcode或是Firebase連接ios app時，都需要Bundle ID去配對
建立App的資訊，除了App名稱外，其他都不能在建立後修改。
```

* 您也可以透過Xcode Archive app時自動產生Bundle ID，自動產生的Bundle ID會出現在下拉選單中，在用此方法您必須先在mac電腦上生產private key和Certificates，並在[apple developer](https://developer.apple.com/account/resources/certificates)進行綁定，綁定過後的mac使用者才能在Xcode上下載iOS Distribution Certificate(記得搭配生產的private key，鑰匙和證書是一對的，沒有private key無法下載)，進行Archive和upload app。
詳請可參考：[開發ios app前的手動設定](https://dotblogs.com.tw/jamestsai/2019/08/27/How-to-set-iOS-Development-Certificates-Identifiers-and-Profiles-by-using-Xamarin-Develop-iOS-App-I)、[Private Key生產的方法](https://medium.com/%E5%BD%BC%E5%BE%97%E6%BD%98%E7%9A%84-swift-ios-app-%E9%96%8B%E7%99%BC%E5%95%8F%E9%A1%8C%E8%A7%A3%E7%AD%94%E9%9B%86/%E8%BC%B8%E5%87%BA%E4%B8%8A%E6%9E%B6-ios-app-%E4%B8%8D%E8%83%BD%E6%B2%92%E6%9C%89%E7%9A%84-private-key-5d935ede10c8)

* 『App Store』中可查看和更改在app store上可看到的資訊欄
![](https://i.imgur.com/6FS5d9S.png)

* 『功能』中有"促銷代碼"與"加密資訊"
![](https://i.imgur.com/X3mib9S.png)

* 『TestFlight』可供依版本做內部測試
![](https://i.imgur.com/Sg6gRuA.png)


* 『活動』中可查看所有從Xcode成功上傳的App
![](https://i.imgur.com/PMj9l6b.png)



# 更改App資訊與提交審查

幾個比較重要的:

1. 更改App名稱
左側App資訊中可以更改App名稱，更改過後記得案右上角儲存，名稱不能跟現有的apple store上的app重複。
![](https://i.imgur.com/fMYRd0R.png)

2. 刪除App
App資訊頁最下面有"移除App"
```
注意：移除app並不是真的移除，官方只是讓此app不能使用而已，以此命名的Bundle ID一樣不能再使用了！
雖然移除之後可以點選回復app，但短時間內不一定真的能回復(官方很多毛病)，請三思再按下刪除！
```
![](https://i.imgur.com/DEx0JcG.png)
3.填妥資訊
將左方"App資訊"、"定價與供應狀況"、"App隱私權"頁面填妥
![](https://i.imgur.com/yKuZoSy.png)


## 填寫審查資訊:
在左側ios App下方選擇(版本號)準備提交填寫資訊

1. 提供各個裝置的 App 螢幕快照
可利用模擬器的拍照功能(command + s)，但要記得先把模擬器縮放到最大(command + 1)再進行拍照，即可拍出符合上傳的尺寸大小。
![](https://i.imgur.com/WNxpjio.png)
2. 填寫行銷宣傳文字、關鍵字、支援 URL、行銷 URL、描述
3. 選擇建置版本(先在Xcode上傳App參照[下一章](#在Xcode封裝上傳App))
4. 填寫版本、版權、年齡分級等等
5. 填寫App 審查資訊
6. 設定版本發佈，可以設定手動發佈、審查完自動發佈、定時發佈
7. 按右上角藍色按紐"提交以供審查"，若設定手動發佈等待官方審查完後會變成"發佈此版本"
![](https://i.imgur.com/gGH1RFB.png)


詳請參考:[[官方文件]輸入App資訊](https://help.apple.com/app-store-connect/#/dev97865727c/)

# 在Xcode封裝上傳App


*以下功能可能會依Xcode改版頁面或名稱會不一樣，但通常都在同一頁*


1. 在Xcode上登入上架帳號(Apple ID)
到 App 的 General 頁面，在 Signing 區塊點選 Add Account登入，登入後將Team選擇為剛剛登入的帳號
![](https://i.imgur.com/iXyf6Se.png)
2. 選擇與環境對應的Schema
* 在General裡可以看到設定App的重要參數
![](https://i.imgur.com/kReY2HV.png)
* 在這個專案裡，這裡的參數都不用手動修改，應由指令同步修改ios和android的version和build號碼，Display name和Bundle Identifier則綁定在環境參數上，只要選擇相對應的環境schema直接按Archive即可。若要修改Displayname請到Build settings頁面修改"App_display_name"。
* 有時候會出現已經選擇新的Schema，但Display name 或 Bundle Identifier 顯示的還是之前build時的參數之情形，這是Xcode的顯示bug，不要自己手動改參數，Xcode會以為你每一次都要自己手動改這個欄位，導致原本綁定"App_display_name"的Display name跳回預設值。
* 如果不幸回到預設值可以到Xcode專案左側目錄中尋找info.plist，將display_name改回${App_display_name}
* 在這裡選擇相對應環境的Schema
![](https://i.imgur.com/RW8348r.jpg)

3. 將 App Build 的對象改為 Generic iOS Device。
如果不改成Generic iOS Device，Archive會是灰色的字(disable)不能按
![](https://i.imgur.com/ehkTMcu.jpg)


4. 點擊 Product > Archive封裝App
Archive一次會花比較長的時間，若Archive跑完有紅色的驚嘆號，那就只能debug完重試，有時候也會發生run的時候不會有錯誤，但Archive完就會跳錯誤的情形。其中比較多會出現的錯誤訊息是『 ld: library not found for -l"packge name"』，代表鏈結package時出現問題，詳情請見：[[RN]ios app未正確linking packge](#react-native-ios-app未正確linking-packge)
![](https://i.imgur.com/Ghbdl2T.png)

5. 上傳完會出現這個視窗，案右邊的藍色按鈕(Distribute app)
![](https://i.imgur.com/HRMuN8W.png)

6. 接下來的畫面，一般不需做任何調整，一直點選 Next 即可
選擇 ios App Store -> Upload -> App Store distribution options頁面(全部勾選)
![](https://i.imgur.com/O2OEyIc.png)
->勾選 Automaticlly manage signing 表示 Xcode 會幫我們自動處理上架 App 需要的 profile，app ID 和 certifcate。
![](https://i.imgur.com/YcPO90w.png)

7. 最後會出現確認畫面，點選Upload上傳
![](https://i.imgur.com/GtHL1OM.png)
![](https://i.imgur.com/nLqkr8P.png)

8. 上傳完可能會出現錯誤訊息，依照錯誤訊息去Xcode加需要的設定
![](https://i.imgur.com/zIHgVkw.png)

9. 順利上傳之後，可以到[apple store connect](https://appstoreconnect.apple.com/apps)『活動』中確認app是否正在上傳
![](https://i.imgur.com/ATwwbBW.png)
![](https://i.imgur.com/i0w4cSq.png)

10. 如果不幸的App上傳到一半消失了，請去信箱看一下apple官方寄的信，裡面會告訴你缺少了哪些apple store上的規範
```
不管上傳成功與否，只要是上傳過的app都會占用一個版號，下一次上傳的version號碼一定要不同於之前的號碼。
```

# [react native] ios app未正確linking packge
錯誤訊息:
```
react native ld: library not found for -l"packgeName"
```

有以下幾種可能:
1. 查一下該package文件，是否該加什麼在podfile文件裡。
例如[React Native Permissions](https://github.com/zoontek/react-native-permissions)中有提到新加入的permission需加在podfile裡，加入後開啟終端機至專案目錄ios資料夾，重新下pod install指令，然後在Xcode打開檔尾為"xcworkspace"的專案，下build clean指令"command+k"，剛剛下載的pod file會重新編譯。
 * 如果還是不行可以把專案目錄下的node_modules資料夾刪除，和ios目錄下的Podfile.lock、pod資料夾刪除，重新下指令，再去Xcode build看看。
```
npm install && cd ios && pod install && cd ..
```
![](https://i.imgur.com/zr0j03e.png)

2. 重新linking
請參考官方文件[Linking Libraries](https://reactnative.dev/docs/linking-libraries-ios)

3. 檢查Libary Search Paths
到Target->Build Settings->搜尋Libary Search Paths->檢查有沒有${inherited}，沒有的話請加上去
* 或是要在這裡直接加上該libary路徑也可以(不推薦)
![](https://i.imgur.com/KUcbt9y.png)
* 為什麼不推薦手動設定呢？因為React native和Xcode都不斷在新版本中嘗試自動鏈接，有越來越改善，雖然還是常常出現沒鏈結的情形(坑)，如果google之後很多人推薦用手動鏈結修好bug的話再使用比較好

4. 更改Workspace Setting
到Files->Workspace Setting->Build system
通常是用"legacy build system"(傳統建構系統)，ios系統升級或是加入新的套件之後也可能會改成"New Build System"(新構建系統)

5. 你可能開錯Xcode專案了
檔尾是"xcworkspace"，不是"xcodeproj"，在ios目錄下重新用Xcode開啟

6. 提供幾個Troubleshooting試試看
* Running Clean in Xcode. (command+shift+k)
* Deleting Xcode's derived data 
到Xcode -> Preferences,切換到Locations分頁，點選Derived Data下方路徑旁指向右邊的箭頭，Finder視窗顯示Derived Data資料夾，把裡面的東西通通刪除(command+delete)
* Removing node_modules then reinstalling dependencies. (rm -rf node_modules && yarn)
* Clearing React Native's packager cache. (react-native start --reset-cache)
* Clearing React Native's iOS build folder. (rm -rf ios/build)
* Updating Pod repos. (cd ios && pod repo update)
* Reinstalling Pods. (cd ios && pod install)

# TestFlight上做內部測試

1. 確認App上傳成功(字不是灰色的)
![](https://i.imgur.com/69LlZUW.png)

2. 到TestFlight點選左邊的內部群組->Apple Store Connect使用者
![](https://i.imgur.com/q0Cdxsd.png)

3. 滑到下面的建置版本，在你要測試的版本狀態欄點選管理
![](https://i.imgur.com/UIxwGwO.png)

4. 兩個視窗都點選"是"，同意條款進行內部測試，黃色驚嘆號變成綠色勾勾表示該版本可以開始測試
![](https://i.imgur.com/S6s3HSt.png)
![](https://i.imgur.com/1NlEz9l.png)

5. 將要進行內部測試人員的email加入[使用者與存取權限](https://appstoreconnect.apple.com/access/users)，對方必須到信箱收邀請信加入(有時限)
![](https://i.imgur.com/977Z6FD.png)

6. 角色建議設為"開發者"才不會一直收到apple寄的app更新信
![](https://i.imgur.com/KF9alQz.png)

7. 回來點選測試人員旁邊的加號，邀請人員加入測試
![](https://i.imgur.com/CtfEubS.png)

8. 被邀請者會在信箱收到TestFlight的的邀請碼，用iphone打開TestFlight App，兌換邀請碼，就可以下載內部測試App。(邀請信時效很短)

