---
layout: post
title: "[jQuery] 自製jQuery Ajax Loader"
date: 2012-12-13 07:01
comments: true
categories: jQuery
---

現代的網頁技術越來越重視Ajax(Asynchronous JavaScript and XML)，很多地方都可以看的到他的身影，最為人所知的就是Google有很多服務都有運用此技術，例如Gmail、Google Map等，在使用Ajax時因為是 **非同步傳輸** 的關係，所以User在傳送資料過程中，可以繼續做其他事情，不過有時候怕User以為按了沒反應認為網頁掛掉，會加上一些Ajax loading來提示網頁還在運作

<!--more-->

以前我最常用到的是 <a href="http://www.malsup.com/jquery/block/#overview" target="_blank">jQuery BlockUI Plugin</a>，但畢竟是別人寫的plugin，總是覺得有些功能有點多餘，雖然jQuery BlockUI大小大概只有18kb左右，但還是總會想要更精簡，做更符合自己想要的plugin出來，找了一些資料以後，大概知道一些運作的原理，下面就來筆記

##Start

首先是html部份

	<div>
	內容
	</div>
	
對..，沒錯，html部份這樣就可以了，其實自製的好處在於是，你不用為了做Ajax loading的效果而特地在HTML上增加額外的元素，所有需要用到的元素都是利用jQuery動態加入，所以保持原本的頁面即可

不過為了展現Demo效果，還是要加上一些css才行

	div{
		background-color: blue;
		height: 800px;
		position: relative;
		width: 100%;
	}
	
接著是js主程式部份

	function ajaxLoader (el, options) {
		// Becomes this.options
		var defaults = {
			bgColor 		: '#fff',
			duration		: 800,
			opacity			: 0.7,
			classOveride 	: false
		}
		this.options 	= jQuery.extend(defaults, options);
		this.container 	= $(el);
		this.init = function() {
			var container = this.container;
			// Delete any other loaders
			this.remove();
			// Create the overlay
			var overlay = $('<div></div>').css({
					'background-color': this.options.bgColor,
					'opacity':this.options.opacity,
					'width':container.width(),
					'height':container.height(),
					'position':'absolute',
					'top':'0px',
					'left':'0px',
					'z-index':99999
			}).addClass('ajax_overlay');
			// add an overiding class name to set new loader style
			if (this.options.classOveride) {
				overlay.addClass(this.options.classOveride);
			}
			// insert overlay and loader into DOM
			container.append(
				overlay.append($('<div></div>').addClass('ajax_loader')).fadeIn(this.options.duration)
			);
		};
		this.remove = function(){
			var overlay = this.container.children(".ajax_overlay");
			if (overlay.length) {
				overlay.fadeOut(this.options.classOveride, function() {
					overlay.remove();
				});
			}
		}
		this.init();
	}
	
大概50行不到的程式碼，這裡說明一下整個運作過程

因為JavaScript並沒有類別，所以這邊用的是建構式函式，之前曾經寫過關於 <a href="http://blog.rx836.tw/blog/javascript-custom-function/">建構式函式</a> 的文章，有興趣的人可以參考看看，我們命名了一個function **ajaxLoader**，裡面有預設值 **defaults**，是在沒有給予 **options** 時會用到的

而 **this.container** 就是要被block的元素，**this.init** 裡面包含的是動態加入Ajax loading的效果，可以看到最主要加了一個&lt;div&gt;進去，給予他透明度(opacity)、背景顏色(background-color)，最最最最最最重要的是把 **z-index** 設成99999，這樣才能讓被block的元素確實達到無法操控，在這個&lt;div&gt;裡面還包了一層&lt;div&gt;是放置載入中的轉圈圈圖片

<img src="https://lh4.googleusercontent.com/-7nndaD_jRSg/UMlDmhEwXEI/AAAAAAAACE0/Jp_u5yf9blY/s31/spinner_squares_circle.gif" />

另外 **this.remove** 就是移除效果，所以整個程式碼其實不難，也沒有其他多餘的阿雜，要使用的時候可以這樣寫

css部份

	.ajax_loader {background: url("spinner_squares_circle.gif") no-repeat center center transparent;width:100%;height:100%;}

預設的轉圈圈圖片
	
js部份

	var options = {
		bgColor 		: '#fff',
		duration		: 800,
		opacity		: 0.7,
		classOveride 	: false
	}
	var block;
	$("div").live('click', function(){
	     block = new ajaxLoader(this, options);
	});
	
**ajaxLoader** 第一個參數可以丟入其他想要被block的元素，第二個就是自訂參數，自訂參數說明如下

<ul>
<li>bgColor: string – 覆蓋的背景顏色</li>
<li>duration: number – fadeIn和fadeOut效果延遲時間</li>
<li>opacity: number – 背景透明度</li>
<li>classOveride: string – 如果想要別的Ajax loading圖片效果，可以加上自訂的class，然後在css自訂樣式即可</li>
</ul>

假如想要移除的話

	block.remove();

想要看更多用法的話可以看這個	<a href="http://www.aplusdesign.com.au/demos/ajax-loader/index.html" target="_blank">Demo</a>

有了這個基本的架構和觀念以後，就可以自己客製化屬於自己的Ajax loading效果，而不必再拘束別人的plugin之下，整個js也輕量許多

###參考資料:

<a href="http://www.aplusdesign.com.au/blog/jquery-ajax-loader-spinner/" target="_blank">jQuery Ajax Loader & Spinner</a>

<a href="http://www.ajaxload.info/" target="_blank">推薦製作gif圖檔的工具-ajaxload.info</a>

內容如有錯誤，歡迎指正