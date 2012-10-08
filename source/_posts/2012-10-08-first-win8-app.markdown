---
layout: post
title: "[Win8] 入門要學說Hello world"
date: 2012-10-08 17:06
comments: true
categories: Win8
---
最近正在練習開發Win8 App，雖然微軟提供的開發途徑很多，例如C#、C++等，但因為自己對JavaScript比較有興趣，而且微軟也提供利用HTML+JavaScript+CSS就可以開發出Win8 APP，所以就決定朝這個方向前進，因為是第一次開發Win8 APP，想當然要先做出一個Hello world來試試看

<!--more-->

要開發Win8 APP，必須先下載工具，直接到微軟官網下載<a href="http://www.microsoft.com/visualstudio/cht/downloads" target="_blank">Visual Studio Express 2012 for Windows 8</a>，安裝完以後，打開就會問你是否需要開發人員授權，輸入帳號密碼，就可以擁有開發人員的帳號

打開Visual Studio Express 2012(以下簡稱VS 2012)，就會看到以下畫面

<img src="https://lh4.googleusercontent.com/-iLMiTXNLEaM/UHKuEKHOTHI/AAAAAAAABsY/DLqeu2umA-M/s786/p1.png" />

接著選【檔案】-> 【新增專案】，就會出現以下的畫面

<img src="https://lh4.googleusercontent.com/-SeFZ08v5dSo/UHKuEndFXlI/AAAAAAAABsc/OKsOpJp0zic/s787/p2.png" />

然後選擇【已安裝的】->【範本】->【JavaScript】->【Windows市集】->【空白應用程式】，接著在專案名稱裡面取名為MyHelloWorld，按下確定

<img src="https://lh5.googleusercontent.com/-EdDsceusOP8/UHKuEz1w-iI/AAAAAAAABsg/49aDvnhF7Ug/s786/p3.png" />

建立好專案以後，會看到VS 2012已經預設建立好一些檔案，例如像package.appxmanifest資訊清單檔案，主要描述應用程式名稱、介紹、啟動顯示畫面，還有logo.png 和 smalllogo.png分別為大的和小的標誌影像，還有代表市集中的影像storelogo.png，和應用程式啟動時顯示的畫面splashscreen.png

其他就是預設的css和js和應用程式啟動時執行的起始頁default.html

按下ctrl+F5啟動應用程式

<img src="https://lh3.googleusercontent.com/-T-_lt_kQehI/UHKuFtbyMpI/AAAAAAAABso/zTQWUiOUyWg/s745/p4.png" />

上面那張圖就是剛剛所提到的啟動顯示畫面圖splashscreen.png

顯示畫面完以後就是主要的APP內容

<img src="https://lh3.googleusercontent.com/-7d-UacNm56o/UHKuF2WBmYI/AAAAAAAABss/xQwqzgpJwVI/s745/p5.png" />

default.html長這樣

	<!DOCTYPE html>
	<html>
	<head>
    <meta charset="utf-8" />
    <title>HelloWorld</title>

    <!-- WinJS 參考 -->
    <link href="//Microsoft.WinJS.1.0.RC/css/ui-dark.css" rel="stylesheet" />
    <script src="//Microsoft.WinJS.1.0.RC/js/base.js"></script>
    <script src="//Microsoft.WinJS.1.0.RC/js/ui.js"></script>

    <!-- HelloWorld 參考 -->
    <link href="/css/default.css" rel="stylesheet" />
    <script src="/js/default.js"></script>
	</head>
	<body>
		<p>內容在此處出現</p>
	</body>
	</html>
	
對於網頁開發者來說一點都不陌生，這也是Win8 APP主打的賣點，接著我們開始來修改一下內容

	<body>
    <h1>Hello, world!</h1>
    <p>What's your name?</p>
    <input id="nameInput" type="text" />
    <button id="helloButton">Say "Hello"</button>
    <div id="greetingOutput"></div>
	</body>
	
在body裡面加上這些html，按下ctrl+f5執行，會發現有文字有按鈕，但還沒有反應，所以接下來就是重頭戲部分，建立事件處理常式，不過建立之前先來看看default.js裡面有些甚麼

	(function () {
		"use strict";

		 // Omitted code 

	 })(); 
	 
預設是將js程式碼包裝在自我執行的匿名函式，有用jQuery的人應該不陌生，主要避免命名衝突或避免意外修改到不想修改的值，use strict代表開啟<a href="http://msdn.microsoft.com/zh-tw/library/windows/apps/br230269.aspx" target="_blank">strict 模式</a>

其餘的程式碼就是APP的事件監控，但目前還用不到，現在我們會看到default.js裡面有個*app.start*，首先在他前面先建立一個click事件

	function buttonClickHandler(eventInfo) {
		var userName = document.getElementById("nameInput").value;
        var greetingString = "Hello, " + userName + "!";
        document.getElementById("greetingOutput").innerText = greetingString; 
    }
	
看起來都跟平常寫網頁的方式都一樣，但建立好事件以後要在哪個時間點註冊這個事件呢？答案就是應用程式啟動時

	var app = WinJS.Application;
    var activation = Windows.ApplicationModel.Activation;
    WinJS.strictProcessing();

    app.onactivated = function (args) {
        if (args.detail.kind === activation.ActivationKind.launch) {
            if (args.detail.previousExecutionState !== activation.ApplicationExecutionState.terminated) {
                // TODO: This application has been newly launched. Initialize
                // your application here.
            } else {
                // TODO: This application has been reactivated from suspension.
                // Restore application state here.
            }
            args.setPromise(WinJS.UI.processAll());           
        }
    };

微軟都已經把Win8 APP許多的事件都已經處理好，我們只要用他的事件處理常式即可，像**app.onactivated **就是應用程式啟動時會觸發的事件，不過裡面其實還有分**第一次啟用**還是**已經啟動但因為擱置而重新啟用**，不過在這裡我們也先暫時不用管是甚麼時候啟用，因為不管如何我們都要註冊點擊這個事件

	    app.onactivated = function (args) {
        if (args.detail.kind === activation.ActivationKind.launch) {
            if (args.detail.previousExecutionState !== activation.ApplicationExecutionState.terminated) {
                // TODO: This application has been newly launched. Initialize
                // your application here.
            } else {
                // TODO: This application has been reactivated from suspension.
                // Restore application state here.
            }
            args.setPromise(WinJS.UI.processAll());

            // Retrieve the button and register our event handler. 
            var helloButton = document.getElementById("helloButton");
            helloButton.addEventListener("click", buttonClickHandler, false);

        }
    };
	
所以會看到我將點擊事件寫在**args.setPromise(WinJS.UI.processAll())**後面，接著一樣按下ctrl+f5，在對話框中輸入名字，就會出現問候語了

<img src="https://lh4.googleusercontent.com/-_NE7vhIsN-w/UHKuGaUHX-I/AAAAAAAABs8/K9SVwBzKgFo/s744/p6.png" />

完成囉！等等，為什麼你的畫面看起來是白色的？大家回去看看default.html有先引用一個CSS檔案進來

	<link href="//Microsoft.WinJS.1.0.RC/css/ui-dark.css" rel="stylesheet" />
	
只要將它改成

	<link href="//Microsoft.WinJS.1.0.RC/css/ui-light.css" rel="stylesheet" />
	
背景就會變成白色的囉！當然這個是官方提供的預設樣式表，文件上是建議用預設的樣式表為基礎去做客製化修改，至於怎麼修改就看大家的APP風格了

官方建議如果是大量的影像或圖片，建議用深色系的css，如果是文字居多，建議用淺色系的css

參考資料:

<a href="http://msdn.microsoft.com/zh-tw/library/windows/apps/hh986964.aspx" target="_blank">建立 "Hello, world" 應用程式</a>


內容如有錯誤，歡迎指正





