---
layout: post
title: "[學習筆記] 如何停止浪費時間在舊版IE的相容性"
date: 2012-10-26 12:25
comments: true
categories: 學習筆記
---

IE的痛...，只有遇過才可以體會到，我相信絕大多數的開發者都曾經有過這個痛，在許多開發者聚會的場合裡面，IE也是最常被拿出來開玩笑，但如何停止浪費你的時間去為了IE做開發上的調整？Mandy Barrington所寫的<a href="http://www.sitepoint.com/how-to-stop-wasting-time-developing-for-internet-explorer/" target="_blank">How to Stop Wasting Time Developing for Internet Explorer</a>或許可以供大家參考

<!--more-->

### 1.使用分析工具

使用分析工具來分析網站的訪客都用哪一個瀏覽器，如果發現只有很少數的人使用舊版IE，就別花費時間去為了那些訪客做修改，在這裡推薦很多網站都使用的<a href="http://www.google.com/analytics/" target="_blank">Google Analytics</a>，最重要的是它還是免費

### 2.提醒用戶升級

假設有些時候某些功能沒辦法在舊版的IE上執行，那善意的提醒也是不錯的效果，可以在這邊下載<a href="http://code.google.com/p/ie6-upgrade-warning/" target="_blank">IE6 Upgrade Warning</a>，這個由Google寫的Project可以幫助你在訪客是使用IE6時，跳出提醒升級的視窗，使用方式就是先下載整包Project，放進你的網站裡面，並且加入以下程式碼

	<!--[if lte IE 6]><script src="js/ie6/warning.js"></script><script>window.onload=function(){e("js/ie6/")}</script><![endif]-->
	
**warning.js**這支檔案可以隨著擺放路徑而調整，假如偵測到訪客是使用IE6就會跳出以下畫面

<img src="https://lh5.googleusercontent.com/-rsWJFxHcHAs/UIoszY9MeOI/AAAAAAAABvg/KV_7bbdkMEg/s700/upgrade.jpg" />

當然你也可以換成繁體中文版，只要打開warning.js這支檔案，將前三行的code換成以下的程式碼即可

	var msg1 = "你知道你的 Internet Explorer 瀏覽器已經過時了嗎？";
	var msg2 = "建議你升級到較新的版本，或是改用其他的瀏覽器，以獲得更好的使用體驗。下面是一份目前廣受歡迎的瀏覽器列表。";
	var msg3 = "只要點選圖示，就可以連到各自的下載頁面。";
	
記得注意UTF-8的編碼問題

### 3.整理問題

有時候好不容易處理過的BUG，記得要記錄起來，不僅造福將來也有可能碰到問題的自己，也可以幫助團隊的其他人，甚至是社群上同樣遇到相同問題的開發者

### 4.提高預算

假如真的遇到客戶要求一定要支援所有瀏覽器....，那就大膽的開口要求提高預算吧！

以上就是作者建議大家的解決方式

IE的相容性問題我想也不是一時可以解決，但至少幾個大型的入口網站(例如Google)已經開始不再支援老舊的IE，而IE6老實說也慢慢的逐漸消失中，微軟似乎也聽見的大家的心聲，至少IE10目前看起來是中規中矩，讓我們還是用樂觀的心情來迎接未來:)

參考資料:

<a href="http://www.sitepoint.com/how-to-stop-wasting-time-developing-for-internet-explorer/" target="_blank">How to Stop Wasting Time Developing for Internet Explorer</a>

<a href="http://code.google.com/p/ie6-upgrade-warning/" target="_blank">ie6-upgrade-warning</a>

內容如有錯誤，歡迎指正


