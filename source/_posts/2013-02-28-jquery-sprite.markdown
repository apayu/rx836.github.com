---
layout: post
title: "[jQ-Plugin] 利用jQuery做CSS Sprite效果"
date: 2013-02-28 20:53
comments: true
categories: jQ-Plugin
---

<img src="https://lh5.googleusercontent.com/-NrgYmV2EGjs/US9R96MMebI/AAAAAAAACSw/nQUtJ_0HHqc/s372/css-sprite.gif" />

為了讓網站對Server的請求次數減少，有些人會運用到 **CSS Sprite** 的技巧，將所有的小圖合併成一張大圖，再利用 **background-position** 來進行定位，但事先的圖片合併規劃，為了算那些位置，不免覺得稍嫌麻煩，但其實有快速合併成大圖的方法，之前曾經寫過一篇<a href="http://blog.rx836.tw/blog/introduce-compass/" target="_blank">[CSS] 用了就無法回頭的Compass</a>，有興趣的人可以參考

<!--more-->

要運用 CSS Sprite 的技巧，要自己撰寫其實也不難，不過善用 <a href="http://yangkun.github.com/jquery-sprite/#usage" target="_blank">Jquery-sprite</a>，可以更容易來做到這件事情

##Start

首先可以從 github 下載 js 檔

<a href="https://github.com/yangkun/jquery-sprite" target="_blank">DOWNLOAD</a>

html部份

	<div id="swap">
		<a href="#"><span class="google-sprite"></span></a>
		<a href="#"><span class="google-sprite"></span></a>
		<a href="#"><span class="google-sprite"></span></a>
		<a href="#"><span class="google-sprite"></span></a>
		<a href="#"><span class="google-sprite"></span></a>
		<a href="#"><span class="google-sprite"></span></a>
		<a href="#"><span class="google-sprite"></span></a>
	</div>
	
js部份

	$('#swap span.google-sprite').each(function(i) {
		var sprite = $(this).sprite(googleOpts).hover(function() {
			sprite.col(6);
		},function() {
			sprite.col(0);
		});
		sprite.row(i);
	});
	
這邊利用 **.each()** 是因為範例有好幾張圖做變化，在每個圖上加上 **.hover()**

###當滑鼠移入時

就會變化到 **sprite.col(6)**，這個指定的位置

###當滑鼠移出時

就會回到 **sprite.col(0)**，這個指定的位置

原理其實就是在大圖上面將每個小圖畫分位置，利用 row 和 col 的概念來變換相對的位置

想看更多的範例可以參考 <a href="http://yangkun.github.com/jquery-sprite/" target="_blank">這裡</a>

##參考資料:

<a href="http://yangkun.github.com/jquery-sprite/" target="_blank">Jquery-sprite</a>

內容如有錯誤，歡迎指正