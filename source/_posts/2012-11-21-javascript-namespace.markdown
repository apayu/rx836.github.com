---
layout: post
title: "[JavaScript] 簡單看命名空間(Namespace)與jQuery原始碼"
date: 2012-11-21 12:09
comments: true
categories: JavaScript
---

網路上JavaScript的library或plugin非常的多，我平常在寫網頁時，有用到別人的plugin都會稍微看一下source code，會發現「Namespace」在JavaScript的世界當中應用相當的廣泛，就連著名的 **jQuery** 也有用到，學習Namespace不僅可以更能看懂別人寫的code，對於增進自己JavaScript的底子也是非常有幫助，可以說不能輕忽他

<!--more-->

有一個情況是這樣子的，今天我寫了一個叫做CheckName()的函式在網頁裡面，而同事因為接手維護，也因為某次的需求也在網頁裡面自己寫了一個CheckName()，這會發生什麼事情呢？如果同事寫的CheckName()在我之後，他將會**覆蓋**我之前寫的CheckName()，反之亦然，這會造成某段使用這個函式的程式碼出錯，所以為了要避免這種情形發生，可以為他們**再取一個名字**，也就是所謂的**命名空間**，但JavaScript本身並沒有這個機制，但可以依靠**物件**來達到這樣的效果

不好的js寫法

	function CheckName() {
		//我寫的
	}
	//很多程式碼
	//很多程式碼
	//很多程式碼
	//很多程式碼
	function CheckName() {
		//.. 同事寫的
	}
	
可以這樣寫

	//建立一個物件
	var apa = {};     
	function CheckName() {
		//我寫的
	}
	//使物件新增一個方法	
	apa.CheckName = CheckName; 
	//要執行時
	apa.CheckName();
	
如果我同事要寫，他也可以這樣子寫

	var gary = {};     
	function CheckName() {
		//同事寫的
	}	
	gary.CheckName = CheckName; 	
	gary.CheckName();	
	
這樣就不會有衝突的問題，另外你有看過這樣的寫法嗎？

	var obj = obj || {};
	
這代表說如果在建立物件之前先檢查有沒有使用過，如果有的話就直接延用之前寫的物件，如果沒有就給空的物件，避免物件重複宣告

在JavaScript強調盡量少用全域變數，多用區域變數，所以有時候我們可以這樣把程式碼包起來

	(function() {
		var a=1; //區域變數
	})();
	
這樣就可以減少全域變數的使用，jQuery的原始碼也是利用這樣的方式

<a href="http://code.jquery.com/jquery-1.8.3.js" target="_blank">jQuery原始碼</a>

	(function( window, undefined ) {
		//...
		//...
		jQuery = function( selector, context ) {
			// The jQuery object is actually just the init constructor 'enhanced'
			return new jQuery.fn.init( selector, context, rootjQuery );
		}
		//...
		//...
		window.jQuery = window.$ = jQuery;
		//...
	})( window );
	
可以看到中間那段jQuery=function( selector, context )就是我們用jQuery最常見的選擇器宣告，也因為這樣我們才能「jQuery(div)」這樣的方式寫jQuery，而「window.jQuery = window.$ = jQuery;」這段就是可以用「$」來代替「jQuery」，這樣對於jQuery有沒有比較了解呢

參考資料:

<a href="http://caterpillar.onlyfun.net/Gossip/JavaScript/Namespace.html" target="_blank">JavaScript Essence: 名稱管理</a>

內容如有錯誤，歡迎指正



