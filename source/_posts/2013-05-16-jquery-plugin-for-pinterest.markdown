---
layout: post
title: "jquery-plugin-for-pinterest"
date: 2013-05-16 12:13
comments: true
categories: jQ-Plugin
---

<img src="https://lh6.googleusercontent.com/-3uQelUPbt2g/UZSmojbUPxI/AAAAAAAACcA/uPWSGQBZYoQ/w170-h167-no/2013-05-16_162143.jpg" />

大部分的網站要與社群做結合，多以FB、G+、Twitter、或是微博等為主，但這幾天看到一篇文章，是連結 **pinterest** 來做為分享圖片的對象，在此特別紀錄下來

<!--more-->

但為了以後的套用方便，我們可以將這部份的需求寫成一個plugin，至於要做甚麼呢？其實很簡單，就是當滑鼠移到圖片時，右下角浮現出 pinterest 分享圖片的小icon

<img src="https://lh6.googleusercontent.com/-3uQelUPbt2g/UZSmojbUPxI/AAAAAAAACcA/uPWSGQBZYoQ/w170-h167-no/2013-05-16_162143.jpg" />

按下以後，就會跳出 pinterest 的登入畫面(假如沒登入的話)，接著就是看要將圖片 pin 到哪個Board

<img src="https://lh6.googleusercontent.com/-XgxZfhKtXHg/UZSmpJlu9TI/AAAAAAAACcI/hrXNi19FHlc/w856-h463-no/2013-05-16_162258.jpg" />

##Start

首先我們需要知道製作 jQuery plugin 的基本樣板

	(function( $ ) {
		$.fn.pinterest = function(options) {
			
			var settings = $.extend( {                    
			}, options);
			
			return this.each(function() {    
			$.fn.pinterest
			});

		};
	})( jQuery );
	
**$.fn.pinterest**就是呼叫這個 plugin 的名稱，所以也可以取自己喜歡的名稱，接著是準備『分享』的小icon

<img src="http://business.pinterest.com/assets/img/builder/builder_opt_1.png" />

不過為了可以方便以後替換，我們可以寫成這樣

	(function( $ ) {
		$.fn.pinterest = function(options) {
			
			var settings = $.extend( {
				//做為參數設定
				'button' : 'http://business.pinterest.com/assets/img/builder/builder_opt_1.png'
			}, options);
				
			return this.each(function() {    
			
			});

		};
	})( jQuery );

	$(document).on('ready', function(){
		//不喜歡預設圖可以直接這樣替換
		$('img#share').pinterest({ button: 'pinterest-alt.png'});
	});


接著我們需要添加一些 html 元素到圖片上面，包括分享的小圖片

	(function( $ ) {
		$.fn.pinterest = function(options) {
			
			var settings = $.extend( {
				'button' : 'http://business.pinterest.com/assets/img/builder/builder_opt_1.png'
			}, options);
						
			return this.each(function() {    
				img = $(this);
				img.wrap('<span class="pin-it" style="position: relative;" />');
				img.parent('span.pin-it').append('<img src="' + settings.button + '" style="display: none;position: absolute; bottom: 20px; right: 20px;cursor: hand; cursor: pointer;" />');
			});
		};
	})( jQuery );

	$(document).on('ready', function(){
		$('img#share').pinterest({ button: 'pinterest-alt.png'});
	});

以上程式內容主要是用一個 span 包起來，再將分享小圖片放置在圖片右下角

接著加上 on_click 和 on_hover_in 事件

	(function( $ ) {
		$.fn.pinterest = function(options) {
			
			var settings = $.extend( {
				'button' : 'http://business.pinterest.com/assets/img/builder/builder_opt_1.png'
			}, options);
			
			function on_click () {         
			};
			
			function on_hover_in() {
				$(this).siblings('img:first').show(500);
			};    
			
			return this.each(function() {    
				img = $(this);
				img.wrap('<span class="pin-it" style="position: relative;" />');
				img.parent('span.pin-it').append('<img src="' + settings.button + '" style="display: none;position: absolute; bottom: 20px; right: 20px;cursor: hand; cursor: pointer;" />');
				img.hover(on_hover_in);
				img.siblings('img:first').on('click', on_click);
			});

		};
	})( jQuery );

	$(document).on('ready', function(){
		$('img#share').pinterest({ button: 'pinterest-small.png'});
	});
	
on_hover_in是讓滑鼠移到圖片時，可以秀出右下角的分享圖片，當然效果可以依照自己喜歡去做修改

至於 on_click 部份，就是將圖片分享致 pinterest

	function on_click () {
		img = $(this).siblings('img:first');
		description = img.attr('title');
		url = document.location;
		media = img.attr('src');

		var pin_url = 'http://pinterest.com/pin/create/button/?url=' + encodeURIComponent( url ) +
			'&media=' + encodeURIComponent( media ) +
			'&description=' + encodeURIComponent( description );
		
		window.open(pin_url, 'Pin - ' + description, 'menubar=no,toolbar=no,resizable=yes,scrollbars=yes,height=600,width=600');
		$(this).hide(1000);
	};

利用 window.open 開啟一個分享視窗，pin_url 裡面的網址搭配參數，分別是

url：從哪個 url 分享而來，利用　document.location　語法取得

media：利用 .attr() 取得該 img 的 src

description：利用 .attr() 取得該 img 的 title

當然，記得使用 encodeURIComponent 做編碼

最後，為了方便 img 的 src 不管是絕對路徑還是相對路徑都可以讓 pinterest 可以使用，要自動加上主機的網址路徑 http://xxx.xxx.com/

	function getUrl(src){
		var url = document.location.toString();
		var http = /^https?:\/\//i;
		if (!http.test(src)) {
			if(src[0] == '/'){
				url = url.substring(0, url.lastIndexOf('/')) + src;
			} else {
				url = url.substring(0, url.lastIndexOf('/')) + '/' + src;
			}
		} else {
			url = src;
		}
		
		return url;
	};
	
這樣只要將 media 那邊的程式碼改成

	media = getUrl( img.attr('src') );
	
就大功告成了

<a href="http://developerdrive.developerdrive.netdna-cdn.com/wp-content/uploads/2013/05/jquery-pinterest1.zip" target=""_blank>完整範例程式碼</a>

##參考資料:

<a href="http://www.developerdrive.com/2013/05/creating-a-simple-jquery-plugin-for-pinterest/" target="_blank">Creating a simple jQuery plugin for Pinterest</a>

內容如有錯誤，歡迎指正