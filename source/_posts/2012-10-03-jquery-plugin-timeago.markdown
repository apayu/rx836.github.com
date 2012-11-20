---
layout: post
title: "[jQ-Plugin] Facebook XXX hours ago的時間生成"
date: 2012-10-03 01:36
comments: true
categories: jQuery jQ-Plugin
---

<a href="http://timeago.yarp.com/" target="_blank">timeago</a>是一套可以快速生成過去發生時間的jQuery plugin，大家應該對於Facebook文字框下方的『xxx hours ago』不會陌生，留言訊息不再只是單純的『x年x月x日 x時x分x秒』，而是可以很貼心的將時間換算給使用者知道，『喔~ 原來這則留言在幾分鐘之前』，這種對User experience來說其實是相當的加分，要實作其實也不難，網路上也有plugin可以方便使用，就趕快來看看如何做出這種效果吧！

<img src="https://lh6.googleusercontent.com/-8eJHMArd3w0/UGxqjpAcHYI/AAAAAAAABqY/Z8lDGoeU_58/s409/1.jpg" />

<!--more-->

首先<a href="http://timeago.yarp.com/jquery.timeago.js" target="_blank">下載</a>timeago，和jQuery一起引用到html裡面

    <script type="text/javascript" src="http://code.jquery.com/jquery-1.8.2.js"></script>
	<script type="text/javascript" src="http://timeago.yarp.com/jquery.timeago.js"></script>
	
接著是html部分

	<abbr class="loaded timeago" title="when you opened the page"></abbr>
	
這個plugin預設是用abbr這個元素，要搭配裡面的title，title屬性待會會存放時間資訊在裡面，接著是js部分

	$(function(){
		prepareDynamicDates();		
		$("abbr.timeago").timeago();		

		function prepareDynamicDates() {
			$('abbr.loaded').attr("title", ISODateString(new Date()));						
		}

		function ISODateString(d){
			function pad(n){return n<10 ? '0'+n : n}
			 return d.getUTCFullYear()+'-'
				  + pad(d.getUTCMonth()+1)+'-'
				  + pad(d.getUTCDate())+'T'
				  + pad(d.getUTCHours())+':'
				  + pad(d.getUTCMinutes())+':'
				  + pad(d.getUTCSeconds())+'Z'
		}		
		
	});

要注意的一點是，要先將時間轉換成<a href="http://zh.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>，ISO 8601是一種國際標準化組織所訂的日期時間表示法，至於要怎麼轉換，網路上已經都有人寫好了，或是直接看上面範例的函式**ISODateString()**

接著將轉換後的時間放到abbr這個元素的title屬性，然後使用.timeago()這個方法即可，這樣一打開網頁，就會顯示

	less than a minute ago
	
過幾分鐘後 就會顯示，

	2 minutes ago
	
代表已經過了兩分鐘，因為timeago不用重整會自動刷新時間

或是你可以直接看我網頁上的DEMO結果如下

『你開始看這篇文章在<abbr class="loaded timeago" title="when you opened the page"></abbr>』
<script type="text/javascript" src="http://code.jquery.com/jquery-1.8.2.js"></script>
<script type="text/javascript" src="http://timeago.yarp.com/jquery.timeago.js"></script>
<script>
	$(function(){
		prepareDynamicDates();		
		$("abbr.timeago").timeago();		

		function prepareDynamicDates() {
			$('abbr.loaded').attr("title", ISODateString(new Date()));						
		}

		function ISODateString(d){
			function pad(n){return n<10 ? '0'+n : n}
			 return d.getUTCFullYear()+'-'
				  + pad(d.getUTCMonth()+1)+'-'
				  + pad(d.getUTCDate())+'T'
				  + pad(d.getUTCHours())+':'
				  + pad(d.getUTCMinutes())+':'
				  + pad(d.getUTCSeconds())+'Z'
		}		
		
	});
</script>

假如你按F5重整就會發現又回到less than a minute ago (除非js的檔案掛掉，才不會顯示)

但如果是不想用現在時間開始計算，而是希望每則發文的時間開始計算呢？一樣html的部分如下

	<abbr class="modified timeago" title="xxx"></abbr>
	
接著是js部分

	$(function(){
	
		$('abbr.modified').attr("title", "2012-10-02T17:30:33Z");
		$("abbr.timeago").timeago();			
		
	});
	
一樣就直接把當初那則發文的ISO 8601的時間丟到title，然後使用.timeago()就可以了

如果你想用更靈活或擴充性更大的plugin，也可以選擇另一款<a href="http://pragmaticly.github.com/smart-time-ago/" target="_blank">Smart Time Ago</a>，靈感就來自於timeago，只是功能更強大

參考資料:

<a href="http://pragmaticly.github.com/smart-time-ago/" target="_blank">Smart Time Ago</a>

<a href="http://timeago.yarp.com/" target="_blank">timeago</a>

如有錯誤，歡迎指正
