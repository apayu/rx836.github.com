---
layout: post
title: "[Facebook] 如何讓Page Tab的Scroll bar消失以及使用錨點?"
date: 2012-09-19 23:53
comments: true
categories: 
---

常常會看到粉絲團裡面的頁籤活動(Page Tab)，都會出現scroll bar，老實說其實有點醜，所以這邊記錄一下怎樣讓Page Tab消失，讓你的頁籤內容有多長，整個Page Tab就有多長，另外順便記錄一下Facebook錨點的問題

<!--more-->

要如何讓Facebook不再出現scroll bar

<img src="https://lh5.googleusercontent.com/-UTpcRBt6434/UFntIvLIR-I/AAAAAAAABhU/QxBuOx2nspc/s803/1.jpg" width="800px"  />

這是某個粉絲團裡面的頁籤活動，可以看到有一個scroll bar在右側，消失的方法就是在body裡面加上overflow

	<body style="overflow:hidden">
	
但這樣其實有個問題，就是scroll bar雖然消失了，但Page Tab被切到了，也就是說下半部的內容會顯示不出來，所以要在加上JavaScript的code上去

	var _app_id = 'xxxx';
    var _api_key = '';
    //初始化
    FB.init({
        appId: _app_id,
        status: true, // check login status
        cookie: true, // enable cookies to allow the server to access the session
        xfbml: true, // parse XFBML        
        oauth: true // enable OAuth 2.0
    });
	
一般來說這是初始化Facebook的JavaScript SDK，緊接著在後面加上

		FB.Canvas.setAutoGrow();
		
這樣就可以讓你Page Tab可以整個顯示出來，而且也不會再出現scroll bar，要注意的是，以前會用**FB.Canvas.setAutoResize**，不過現在不要再用這個語法囉，因為Facebook已經要刪除，不再支援這種寫法

## Facebook 錨點無效

我們平常寫網頁，我們會這樣設錨點

	<a name="h">我是錨點</a>
	
接著會下這樣的超連結

	<a href="#h">點我跳到我是錨點</a>
	
這樣就可以到達網頁設定好的錨點，但是這樣在Facebook是無效的！因為Facebook Page Tab其實是一個iframe，所以Facebook自己有出SDK可以控制scroll的移動，寫法如下

	FB.Canvas.scrollTo(0, 0);
	
等於說你可以寫click某個HTML讓他移動到你設定好的座標位置，例如

	$('a').click(function(){
		FB.Canvas.scrollTo(0, 300);
	});
	
這樣意思代表點擊a移動到Page Tab坐標(0, 300)的地方，這樣就可以取代錨點失效的問題了

參考資料:

<a href="https://developers.facebook.com/docs/reference/javascript/FB.Canvas.scrollTo/" target="_blank">FB.Canvas.scrollTo</a>

<a href="https://developers.facebook.com/docs/reference/javascript/FB.Canvas.setAutoGrow/" target="_blank">FB.Canvas.setAutoGrow</a>

如有錯誤，歡迎指正

