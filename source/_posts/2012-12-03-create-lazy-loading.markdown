---
layout: post
title: "[jQ-Plugin] 圖片延遲加載-Lazy-Loading"
date: 2012-12-03 15:01
comments: true
categories: jQ-Plugin
---

<img src="https://lh4.googleusercontent.com/-9VL-bSTiio8/ULxO_q7aPbI/AAAAAAAACAQ/R6Nns5e2_T0/s551/qwer.jpg" />

延遲加載圖片常用在有大量圖片的網站，在訪客還沒看到的區域先暫停讀取圖片，等到看到特定區域時才將需要的圖片載入，好處是可以減少一開始等待所有圖片載入的時間，避免訪客感到不耐煩而流失，要做到此效果只需要搭配簡單的jQuery plugin，並且在HTML上加點技巧即可，重點是，要加上這個效果對設計師來說並不困難，因為裡面並沒有涉及到太多JavaScript知識

<!--more-->

##Start

首先必須下載jQuery和<a href="https://raw.github.com/tuupola/jquery_lazyload/master/jquery.lazyload.min.js" target="_blank">minified lazyload script</a>，並且加掛在網頁裡面

	<script src="jquery.js" type="text/javascript"></script>
	<script src="jquery.lazyload.js" type="text/javascript"></script>
	
接著我們需要建立一個 1x1 px的灰色小圖，這將會取代尚未讀取到的圖片，來做為延遲加載的效果

<img src="https://lh4.googleusercontent.com/-GynYPKkHJnU/ULxbNG8liyI/AAAAAAAACA0/QMBzvG46740/s530/rtyu.jpg" />

接著是HTML部分

	<div class="frame"><img class="lazy" src="img/g.gif" data-original="img/interior_01.jpg" width="500" height="333" alt="interior shot #1"></div>

這邊特別的是&lt;img&gt;的屬性 **src** 並不是指向原始圖檔，而是 1x1 px的小圖，而原始圖檔擺放的位置在屬性 **data-original** 裡面，另外要給予原始圖檔的 **width** 和 **height**，避免不必要的錯誤發生

###noscript

在瀏覽器沒有開啟JavaScript的情況下，我們可能也要做一些預防措施，直接將圖片載入，不然使用者看到的圖片都是一片灰

	<div class="frame"><img class="lazy" src="img/g.gif" data-original="img/interior_01.jpg" width="500" height="333" alt="interior shot #1"></div>
	<noscript><img src="img/interior_01.jpg" width="500" height="333" alt="interior shot #1"></noscript>
	
接著是JS部分

	$("img.lazy").lazyload();
	
大功告成！很容易吧，假如你不太喜歡這麼呆滯的載入圖片，可以加入一些效果，例如 **fadeIn**

	$("img.lazy").lazyload({
		effect: "fadeIn"
	});
	
想要看更多運用，可以連到參考資料

###參考資料:

<a href="http://speckyboy.com/2012/10/18/how-to-create-lazy-loading-images-for-your-website/" target="_blank">How to Create Lazy-Loading Images for your Website</a>

<a href="http://www.appelsiini.net/projects/lazyload" target="_blank">Lazy Load Plugin for jQuery</a>

內容如有錯誤，歡迎指正