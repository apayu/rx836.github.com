---
layout: post
title: "[CSS3] 利用transform替網頁做小巧思"
date: 2013-06-11 17:37
comments: true
categories: CSS
---

 
<img src="http://farm4.staticflickr.com/3748/9013398826_44a5b35f7e_o.jpg" />

最近看到一個<a href="http://www.jiawin.com/demos/530/index.html" target="_blank">網站</a>，很酷的將許多CSS3給呈現出來，讓我開始思考怎麼運用在實做的網站上面

<!--more-->

但其實在這之前就做過類似的 CSS3 動畫學習筆記 - <a href="http://blog.rx836.tw/blog/css3-transitions-guide/" target="_blank">[CSS3] 認識CSS3 Transitions</a>，原理其實相差不
遠，不過那時並不知道可以運用在什麼地方，而這次發現可以將轉動的效果，運用在一些點擊的icon上面，讓網站較為活潑，而不再單調，當然，以下的動畫運用Flash也可以簡單的做到，但這
就不在這裡的討論範圍裡面，畢竟條條大路通羅馬

##Start

我這裡運用的實例是，所謂的 lightbox(燈箱) 上面，常常可以看到在一些活動網站，點擊像活動辦法這種連結，就會有可能出現這樣的呈現方式

<img src="http://farm4.staticflickr.com/3748/9013398826_44a5b35f7e_o.jpg" />

而這時候右上角通常都會有可以關閉的X按鈕，點擊後整個視窗就會消失，但為了讓這個 lightbox 不至於太過呆版，可以在關閉X按鈕上面加點巧思

首先是HTML部份
	
	<div id="pop">
		<a id="close"></a>
		我是一個pop視窗我是一個pop視窗我是一個pop視窗我是一個pop視窗我是一個pop視窗
		我是一個pop視窗我是一個pop視窗我是一個pop視窗我是一個pop視窗我是一個pop視窗
		我是一個pop視窗我是一個pop視窗我是一個pop視窗我是一個pop視窗我是一個pop視窗	
	</div>

這是一個常見的 lightbox 結構，當然不一定會長這樣

CSS部份

	#close {
		background: url("http://farm8.staticflickr.com/7282/9011998137_f2d70ac0f8_o.png") no-repeat scroll 0 0 transparent;
		height: 32px;
		position: absolute;
		right: 1px;
		top: 1px;
		width: 32px;
	}
	
	#pop {
		background-color: #C5FF40;
		height: 150px;
		padding: 40px 0 0;
		position: relative;
		width: 500px;
	}
	
簡單的用一個 &lt;div&gt; 包住內容和x關閉按鈕，關閉按鈕是用 &lt;a&gt; 來做，加上背景圖案，接著就是整個動畫的重點所在

	a#close:hover {
		-webkit-animation:example 1s ease 0s alternate none infinite;
		-moz-animation:example 1s ease 0s alternate none infinite;
		animation:example 1s ease 0s alternate none infinite;
	}	
	
	@-webkit-keyframes example { from{-webkit-transform:rotate(0deg); } to{-webkit-transform:rotate(360deg); } }
	@-moz-keyframes example { from{-moz-transform:rotate(0deg); } to{-moz-transform:rotate(360deg); } }
	@keyframes example { from{transform:rotate(0deg); } to{transform:rotate(360deg); } }
	
關鍵在於做 hover 時，觸發 animation，至於裡面的屬性可以參考我之前寫的 <a href="http://blog.rx836.tw/blog/css3-transitions-guide/" target="_blank">文章</a> 或是參考
<a href="http://www.w3schools.com/css3/" target="_bank">w3schools.com</a>，這裡不多加說明

可以發現當滑鼠移到x關閉按鈕時，會有旋轉的效果

<a href="http://jsfiddle.net/sWUVv/" target="_blank">範例</a>

這樣不僅可以提升使用者經驗，也可以讓網頁不在單調

當然我相信一定還有許多CSS3應用，等待著你我發掘:)

##參考資料:

<a href="http://www.w3schools.com/css3/" target="_blank">CSS3 教程</a>

<a href="http://www.jiawin.com/demos/530/index.html" target="_blank">http://www.jiawin.com/demos/530/index.html</a>

內容如有錯誤，歡迎指正
