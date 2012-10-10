---
layout: post
title: "[PhoneGap] 第一次開發PhoneGap教學筆記"
date: 2012-10-10 22:39
comments: true
categories: PhoneGap
---
很早很早以前曾經摸過一下Android，還曾想過要走開發手機這條路，但最後還是繼續寫著網頁，不知道選擇對不對，不過至少現在可以用寫網頁的方式做出APP，那就是利用已經出很久的PhoneGap，但到今天才真正的開始學習他，在這邊也會開始慢慢記錄一些有關於PhoneGap的心得

<!--more-->

網路上已經有很多很多的觀念與介紹，所以這邊就不在多述，要開始之前請先安裝<a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java 開發工具包( Java Development Kit , JDK )</a>，建議大家下載JDK6

<img src="https://lh3.googleusercontent.com/-O98JK3DRzHM/UHWWC5uq4QI/AAAAAAAABtY/ABoTETFnIJo/s538/1.png" />

安裝好以後接著就下載並安裝<a href="http://www.eclipse.org/downloads/" target="_blanl">Eclipse</a>，Eclipse是一個IDE，一個整合開發環境，類似Microsoft Visual Studio，因為Android官方並沒有推出專屬的手機應用程式開發軟體，但有支援 Eclipse 的官方外掛開發套件

<img src="https://lh6.googleusercontent.com/-vDbyAlgXX8M/UHWWDDRPM3I/AAAAAAAABtg/nsLxVsp43L0/s731/2.png" />

以上的安裝和設定過程，都可以參考<a href="http://blog.chinatimes.com/tomsun/archive/2011/11/08/1029787.html" target="_blank">[Android 教學] Android 4.0 SDK 下載安裝中文教學課程講義</a>

接著就是下載本篇主角<a href="http://www.phonegap.com/download" target="_blank">PhoneGap</a>，下載以後進行解壓縮

但其實PhoneGap官方網站有詳細的<a href="http://docs.phonegap.com/en/2.1.0/guide_getting-started_android_index.md.html#Getting%20Started%20with%20Android" target="_blank">入門教學</a>，這裏我就直接按照他的步驟敘述

1.首先開啟Eclipse，選擇**New Project**

2.選擇new一個**Android Application Project**

3.輸入**Application Name**、**Project Name**和**Package Name**

4.設定應用程式icon

5.建立一個**Blank Activity**

6.在你的Android專案裡面建立新的目錄，分別是

	/libs
	assets/www
	
7.從剛剛下載的PhoneGap的資料夾裡面，找到**lib/android/**，並且複製**cordova-2.0.0.js**到**assets/www**資料夾底下

8.複製**cordova-2.0.0.jar**到**/libs**底下

9.複製整個**xml**這個資料夾到Android專案底下的**/res**資料夾

10.針對剛剛的**cordova-2.0.0.jar**檔案按下右鍵，選擇**Build Paths/ > Configure Build Path**，切換到Libraries這個頁籤，將**cordova-2.0.0.jar**加入到裡面

11.找到**src**資料夾底下，副檔名為java的檔案並且開啟編輯他

增加**import org.apache.cordova.*;**這行程式

修改class's extend從Activity改成DroidGap

將**setContentView()**這行取代成**super.loadUrl("file:///android_asset/www/index.html");**
	
12.接著點擊**AndroidManifest.xml**選擇**Open With > Text Editor**

13.將以下程式加到**<uses-sdk.../>**和**<application.../>**tags之間

	<supports-screens 
    android:largeScreens="true" 
    android:normalScreens="true" 
    android:smallScreens="true" 
    android:resizeable="true" 
    android:anyDensity="true" />
	<uses-permission android:name="android.permission.VIBRATE" />
	<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
	<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
	<uses-permission android:name="android.permission.ACCESS_LOCATION_EXTRA_COMMANDS" />
	<uses-permission android:name="android.permission.READ_PHONE_STATE" />
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.RECEIVE_SMS" />
	<uses-permission android:name="android.permission.RECORD_AUDIO" />
	<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
	<uses-permission android:name="android.permission.READ_CONTACTS" />
	<uses-permission android:name="android.permission.WRITE_CONTACTS" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /> 
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.BROADCAST_STICKY" />

14.將以下程式加到**<activity../>**這個tag裡面

	android:configChanges="orientation|keyboardHidden|keyboard|screenSize|locale"

15.新增一個**index.html**到**assets/www**資料夾底下，裡面的html碼為

	<!DOCTYPE HTML>
	<html>
	<head>
	<title>Cordova</title>
	<script type="text/javascript" charset="utf-8" src="cordova-1.9.0.js"></script>
	</head>
	<body>
	<h1>Hello World</h1>
	</body>
	</html>

接下來就可以點擊專案名稱右鍵，選擇**Run As > Android Application**，開始看結果囉！

假如你沒有AVD可以看<a href="http://blog.chinatimes.com/tomsun/archive/2011/11/24/1054452.html" target="_blank">這篇</a>教學怎麼設定AVD

這樣index.html裡面就是你的Android應用程式的內容了，可以用你熟悉的html+css+js來開發手機應用程式

參考資料:

<a href="http://cire.pixnet.net/blog/post/37927775-%5B%E7%AD%86%E8%A8%98%5D--%E7%AC%AC%E4%B8%80%E6%AC%A1%E9%96%8B%E7%99%BC-android-%E7%89%88%E6%9C%AC-phonegap--%2B-jquery-" target="_blank">[筆記] 第一次開發 Android 版本 PhoneGap + JQuery Mobile 就上手</a>

<a href="http://docs.phonegap.com/en/2.1.0/guide_getting-started_android_index.md.html#Getting%20Started%20with%20Android" target="_blank">Getting Started with Android</a>

<a href="http://www.eclipse.org/" target="_blank">eclipse</a>

<a href="http://blog.chinatimes.com/tomsun/archive/2011/11/08/1029787.html" target="_blank">[Android 教學] Android 4.0 SDK 下載安裝中文教學課程講義</a>

<a href="http://blog.chinatimes.com/tomsun/archive/2011/11/24/1054452.html" target="_blank">[Android 教學] Android 4.0 模擬器安裝設定教學課程講義</a>


內容如有錯誤，歡迎指正