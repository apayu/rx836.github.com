---
layout: post
title: "[jQ-Plugin] 在網站中加入星星評分效果"
date: 2013-01-29 11:46
comments: true
categories: jQ-Plugin
---

<img src="https://lh4.googleusercontent.com/-p5vCtEt386M/UQdsNizReKI/AAAAAAAACQs/tylpU5zwd60/s188/2013-01-29_114734.jpg" />

評分功能常出現在一些商品陳列網站，像這種透過選幾顆星星來做評價，在許多網站都看的到，例如 <a href="http://tw.movie.yahoo.com/" target="_blank">YAHOO! 奇摩電影</a> 就有類似的功能，而這篇就是來介紹如何用 jQuery plugin- jStarbox 來實現這項應用

<!--more-->

##Start

jStarbox檔案不到6k，算是相檔的輕巧，css樣式也不多，不會有那種讓人不知道如何修改起的煩惱，source code 可以直接去 github 下載回來

<a href="https://github.com/sabberworm/jStarbox#getvalue" target="_blank">DOWNLOAD SOURCE</a>

裡面有兩個資料夾分別是 images 和 css，還有一個 jstarbox.js 檔案，直接載入 css 和 js 檔到專案裡面，當然 jQuery 也不要忘了

	<link href="css/jstarbox.css" rel="stylesheet"></link>
    <script type="text/javascript" src="http://code.jquery.com/jquery-1.8.2.js"></script>
	<script src="jstarbox.js"></script>
	
接下來是 html 部份

	<div class="starbox">
	</div>
	
沒看錯，只要放個空元素在 html 上即可，並且給他一個 class 名稱方便等下操作，最後是 js 部份

	$('.starbox').starbox({
		average: 0.5,
		changeable: 'once',
		autoUpdateAverage: true,				
		ghosting: true
	});
	
這樣就大功告成囉

###參數設定

以下是一些參數的講解，但有些小弟才疏，也不太懂他的意思就不寫出來誤導大家Orz，有興趣的各位再請去 github 上面看

**average**:可以預設一開始顯示幾顆星星，也可以使用小數點，例如0.4，預設值則是0.5

**stars**:設定有幾顆星星可以選擇，預設值是5

**buttons**:設定星星可以切割成多少區塊可以選擇，假設有5顆星星，buttons設10，每顆星星就可以選擇半顆或整顆

**changeable**:設定選擇以後是否還可以改變

也有一些方法可以呼叫，例如要得知 User 選了幾顆星星，就可以這樣寫

	$('.btn').click(function(){
		alert($('.starbox').starbox("getValue"));
	});
	
可以把事件寫在某個按鈕裡面，當按下按鈕就秀出值是多少，關鍵在這句 

	$('.starbox').starbox("getValue")

##小小總結

如果用 firebug 看套用效果後的 html 結構，不難發現只是在空元素裡面增加幾個&lt;div&gt;，並且設定背景圖做為星星，所以要修改的話只要改範例裡面的圖，和 css 裡面的樣式即可

	.starbox .stars .star_holder .star {
		background-image: url('../images/5-large.png');
		width: 33px;
		height: 33px;
	}
	
記得如果星星的大小有改變，width和 height 也要跟著調整

##參考資料:

<a href="https://github.com/sabberworm/jStarbox#getvalue" target="_blank">jStarbox</a>

<a href="http://sabberworm.github.com/jStarbox/" target="_blank">Examples</a>

內容如有錯誤，歡迎指正