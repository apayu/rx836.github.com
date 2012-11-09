---
layout: post
title: "[PhoneGap] 如何搭配平板或手機開發Android"
date: 2012-11-09 14:32
comments: true
categories: PhoneGap
---

繼好幾天前開始了<a href="http://blog.rx836.tw/blog/phonegap-first/" target="_blank">第一次的PhoneGap之旅</a>，漸漸的開始慢慢熟悉運作模式，有一直寫下去果然還是有差，當然一路上也一直碰到牆壁和踩到地雷(渾身傷..)，這篇就來記錄怎麼用實機做開發測試，往後也會多寫幾篇關於PhoneGap開發心得文章出來奉獻

<!--more-->

雖然之前的文章有提到Android模擬器，但其實每次要把Android模擬器啟動起來還是很不方便，因為總是要等一段時間

<img src="https://lh6.googleusercontent.com/-mBxqTZDV0AI/UJy7d2-dqXI/AAAAAAAAB4Y/hRTlohLYjm4/s630/a1.jpg" />

但如果手邊有Android實機的話(不管是平板還是手機)，都可以用下面的方法來做開發測試(可能會因為改版關係略有不同)

### 1.找找之前下載的Android SDK

相信之前在開發Android的時候，會先下載Android SDK，找找那個SDK，裡面的資料會長的像這樣

<img src="https://lh5.googleusercontent.com/-ny6p8foNJJQ/UJy7dTQ4C5I/AAAAAAAAB4Q/1rL70M7D2-Y/s232/a2.jpg" />

### 2.開啟Eclipse

找到Android SDK以後，打開Eclipse，選擇「Window」->「Android SDK Manager」

<img src="https://lh3.googleusercontent.com/-F24YqktQKuE/UJy7d6jaMCI/AAAAAAAAB4c/5UL63BEf9Zs/s601/a3.jpg" />

### 3.安裝「Google USB Driver」

拉到下面的「Extras」底下有個「Google USB Driver」，勾選並且點選右下角的「install packages...」，注意，因為我是已經安裝過所以才會變淺色，還沒安裝可以進行點選安裝

<img src="https://lh4.googleusercontent.com/-7zkUd652OBw/UJy7eZ6Q1cI/AAAAAAAAB4g/WcSKd8rR0sc/s703/a4.jpg" />

### 4.開啟設備上的USB測試功能

安裝好後接著關閉Eclipse，在來這個步驟，會因為每個人設備不同而稍微有異，舉Nexus 7為例，在「設定」->「開發人員選項」，進去後點右上角的開啟，還有把「USB偵錯模式」勾選起來，其他設備大同小異，接著用USB跟電腦接上，這時電腦會出現安裝驅動程式，先不用管他

### 5.安裝你的硬體驅動程式

接上USB後打開「控制台」->「系統及安全性」->「系統」->「裝置管理員」，會看到可攜式裝置那邊，會有你的設備名稱，並且顯示驚嘆號，在設備上點選右鍵，選擇「更新驅動程式軟體」，接著選擇「瀏覽電腦上的驅動程式軟體」，還記得剛剛安裝的Google USB Driver嗎？位置沒變動會在 Android SDK\extras\google\usb_driver，接著電腦就會自動安裝設備囉~

### 6.令人期待的一刻！

來到最後一個步驟囉，打開Eclipse，編輯AndroidManifest.xml，將以下程式加入到＜application＞這個Tag裡面

	android:debuggable="true"

接著在上面的選單列選擇「Run」->「Run Configurations」，做一些簡單的設定，選擇頁籤「Target」並且點選「Always prompt to pick device」，最主要是因為這樣每次在Run的時候都可以先選擇設備

<img src="https://lh5.googleusercontent.com/-I0yrNYdm1RY/UJy7e8giz5I/AAAAAAAAB40/Hdkv8Ncs-2s/s702/a5.jpg" />

設定好後，點選「Run As」->「Android Application」，如果點選Run As沒有出現Android Application代表你沒有選到專案(看左邊那個紅框)，這也是我一直撞牆的地方...

<img src="https://lh3.googleusercontent.com/-nG-rVob0H0k/UJy7fECMaCI/AAAAAAAAB4w/q1Yp2Is_jQg/s1027/a6.jpg" />

看到你的設備了嗎？別懷疑！直接點選OK開啟吧！

<img src="https://lh5.googleusercontent.com/-gHQrLAMHp_0/UJy7ff6GWmI/AAAAAAAAB4s/ZKxtK4zOfLI/s708/a7.jpg" />

有看到你的手機上顯示畫面出來了嗎？！

有的話就恭喜你！成功囉~，一起加入開發Android吧！

假如不幸失敗的話...，請歡迎留言給我，一起討論(因為你的問題也可能是我的問題..)

參考資料:

<a href="http://developer.android.com/sdk/win-usb.html#WinUsbDriver" target="_blank">Google USB Driver</a>

<a href="http://www.ibm.com/developerworks/cn/web/wa-mobappdev1/index.html" target="_blank">第 1 部分: Android 上的 PhoneGap 和 Dojo Mobile</a>

內容如有錯誤，歡迎指正