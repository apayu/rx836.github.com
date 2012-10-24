---
layout: post
title: "[jQuery] jQuery你一定要知道的八件事"
date: 2012-10-24 23:18
comments: true
categories: jQuery
---

jQuery這項技能在面試的時候，已經從"加分"變成"必備"，由此可知，如果想走web開發，jQuery已經是不可或缺的技術，但jQuery雖然好上手，網路上的教學資源也很多，但有幾件事情是在使用jQuery你一定要知道的

<!--more-->

## 1.使用Google CDN-hosted並且保持最新版本

使用Google CDN的好處是，有許多網站都有使用CDN，所以訪客在拜訪你的網站之前，可能已經先下載過jQuery，之後拜訪你的網站就可以直接從快取中使用，而不用重新下載，增加網站讀取速度，至於保持jQuery最新的版本，除了可以修復一些bug，還可以增加performance

	<script type="text/javascript" src="//ajax.googleapis.com/ajax/libs/jquery/1.8.1/jquery.min.js"></script>
	
有些人可能會發現，為什麼少了**http:**，原因是假如網站遊走在http和https之間，使用這種忽略 **scheme** 的部分，就可以避免因為開啟了https的網頁，但jQuery是http所產生的安全性問題

## 2.在開發時搭配Cheat Sheet

其實不只是初學者，對於資深的開發者也建議使用cheat sheets，可以方便直接查詢，也省去google的麻煩

<a href="http://oscarotero.com/jquery/" target="_blank">http://oscarotero.com/jquery/</a>

<a href="http://www.javascripttoolbox.com/jquery/cheatsheet/" target="_blank">http://www.javascripttoolbox.com/jquery/cheatsheet/</a>

<a href="http://devcheatsheet.com/tag/jquery/" target="_blank">http://devcheatsheet.com/tag/jquery/</a>

## 3.不能單純只使用CDN

剛剛第一點講到建議使用Google CDN，但有一點必須要注意的是，CDN有時候會有失效的問題，像某些地區會連不到Google CDN，這時候就要有locally的jQuery可以備用，判別的JavaScript語法可以這樣寫

	<script src="//ajax.googleapis.com/ajax/libs/jquery/1.8.1/jquery.min.js"></script>
	<script>window.jQuery || document.write('<script src="js/jquery-1.8.1.min.js"><\/script>')</script>
	
這段程式碼會在抓不到Google CDN時，去抓取自家主機上的jQuery，讓網站不至於因為這樣而掛掉

## 4.重複使用jQuery selector

為了優化jQuery，千萬不要這樣寫

	$("#mySmashingID").css("color", "pink");
	$("#mySmashingID").css("font", "Verdana");
	$("#mySmashingID").text("Some error message goes here!");
	
假如要針對同個selectors做操作，不應該重複呼叫自己，而是要利用jQuery鏈結的特性串起來

	$("#mySmashingID").css({ "color": "pink", "font": "Verdana"}).text("Some error message goes here!!");
	
## 5.將重複使用的selector宣告一個變數存起來

假如你會針對一個selector在很多地方使用到

	$(‘#mySmashingGag’).appendTo(‘#mysidebar’);
	$(‘#mySmashingGag’).addClass(‘widget’);
	$(‘#mySmashingGag’).hide();
	$(‘#mySmashingGag’).fadeIn(‘fast’);
	
你應該將他存入一個變數，並且使用變數來操作，這樣也可以增加效能，而不會一直去做selector

	var mySmashingGag = $(‘#mySmashingGag’);
	mySmashingGag.appendTo(‘#mysidebar’);
	mySmashingGag.addClass(‘widget’);
	mySmashingGag.hide();
	mySmashingGag.fadeIn(‘fast’);
	
## 6.使用ID而不要使用class

jQuery骨子裡其實還是JavaScript，所以不管如何速度再快也比不上原生的JavaScript快，所以如果使用ID來選取元素的話，就會使用JavaScript的原生方法 **getElementByID**，效能就會比較快，相反的不是使用原生方法的class效能就會比較慢

不要使用class

	// Selecting each item at once
	for (i = 0; i < 900; i++) {
		var selectedItem = $('.mySmashingItem' + i);
	}
	
使用ID

	// Selecting each item at once
	for (i = 0; i < 900; i++) {
		var selectedItem = $('#mySmashingItem' + i);
	}
	
## 7.使用縮寫

正常來說會這樣寫

	$(document).ready(function (){
		// your awesome code here
	});
	
但其實可以這樣寫

	$(function (){
		// your awesome code here
	});
	
## 8.使用context

當你再使用選取器(selectors)的時候，jQuery會針對整個頁面去做搜索直到找到為止，可是其實我們可以縮小範圍

例如原本的寫法

	$(‘.mySmashingGag’).on(‘click’, showMenu);
	
但我們可以這樣寫

	$(‘.mySmashingGag’, ‘#mySidebar’).on(‘click’, showMenu);
	
這樣他就會在ID為mySidebar去搜尋class為mySmashingGag的元素

這些其實不難，但都是養成正確寫jQuery的好習慣:)

參考資料:

<a href="http://smashinghub.com/8-jquery-crimes-you-really-shouldnt-commit.htm" target="_blank">8 jQuery Crimes You Really Shouldn’t Commit</a>

<a href="http://blog.miniasp.com/post/2008/10/19/URL-URI-Description-and-usage-tips.aspx" target="_blank">講解 URL 結構與分享幾個相對路徑與絕對路徑的開發技巧 </a>

內容如有錯誤，歡迎指正