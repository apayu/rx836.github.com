---
layout: post
title: "[jQuery] 利用CSS3 3D Transforms做翻書效果 Flip Plugin"
date: 2012-09-06 12:04
comments: true
categories: 
---

在網路上看到<a href="http://tympanus.net/Development/BookBlock/" target="_blank">翻書效果</a>感覺蠻有趣的，是利用<a href="http://www.w3schools.com/css3/css3_transitions.asp" target="_blank">CSS3 Transitions</a>和<a href="http://www.w3schools.com/css3/css3_3dtransforms.asp" target="_blank">CSS3 3D Transforms</a>的效果實現，這裡我是用<a href="http://tympanus.net/codrops/2012/09/03/bookblock-a-content-flip-plugin/" target="_blank">Flip Plugin</a>

<!--more-->

因為已經有<a href="http://tympanus.net/Development/BookBlock/BookBlock.zip" target="_blank">範例檔</a>可以用，所以就不詳細講太多程式碼細節，首先先載入CSS和Modernizr，這兩隻檔案在範例檔裡面都有，分別在css和ja的資料夾裡面

	<link rel="stylesheet" type="text/css" href="style.css" />
	<link rel="stylesheet" type="text/css" href="custom.css" />
	<script type="text/javascript" src="modernizr.custom.79639.js"></script>
	
可以看到CSS其實就是一開始先將第一張照片秀出，其他都先**display : none**，至於modernizr是因為為了要支援IE9以下所用的，因為IE9以下不支援CSS3 Transitions和CSS3 3D Transforms，所以要利用modernizr來偵測User所用瀏覽器的支援程度來決定實現的效果

接下來要引用其他三支js進來

	<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.8.1/jquery.min.js"></script>
	<script type="text/javascript" src="jquerypp.custom.js"></script>
	<script type="text/javascript" src="jquery.bookblock.js"></script>
	
其中jquerypp.custom.js是<a href="http://jquerypp.com/" target="_blank">jQuery++</a>，擴充了**swipe even**這個功能，讓行動裝置用手指滑動也能觸發翻頁的效果

而jquery.bookblock.js就是Flip Plugin，我們可以看到裡面其中一行是

	this.support = Modernizr.csstransitions && Modernizr.csstransforms3d;
	
這行就是利用Modernizr在檢查User現在的瀏覽器支援程度，所以下面就會有if判斷

	if( !this.support ) {
		
		this._layoutNoSupport( dir );

	}
	else {

		this._layout( dir );

	}
	
假如不支援的話，就會用.hide() or .show()來實現換頁效果，如果有支援就會使用CSS3 3D Transforms

接著是基本HTML架構

	<div id="bb-bookblock" class="bb-bookblock">
		<div class="bb-item">
			<!-- custom content -->
		</div>
		<div class="bb-item">
			 
		</div>
		<div class="bb-item">
			<!-- ... -->
		</div>
		<div class="bb-item">
			<!-- ... -->
		</div>
		<!-- ... -->
	</div>

**bb-item**就是裡面每一頁要放的內容，可以是圖片或文字

而js部分可以這樣寫

	$(function() {
				 
		$( '#bb-bookblock' ).bookblock();
	 
	});
	
裡面的options設定如下

	// speed for the flip transition in ms.
	speed       : 1000,
	 
	// easing for the flip transition.
	easing      : 'ease-in-out',
	 
	// if set to true, both the flipping page and the sides will have an overlay to simulate shadows
	shadows     : true,
	 
	// opacity value for the "shadow" on both sides (when the flipping page is over it).
	// value : 0.1 - 1
	shadowSides : 0.2,
	 
	// opacity value for the "shadow" on the flipping page (while it is flipping).
	// value : 0.1 - 1
	shadowFlip  : 0.1,
	 
	// perspective value
	perspective : 1300,
	 
	// if we should show the first item after reaching the end.
	circular    : false,
	 
	// if we want to specify a selector that triggers the next() function. example: '#bb-nav-next'.
	nextEl      : '',
	 
	// if we want to specify a selector that triggers the prev() function.
	prevEl      : '',
	 
	// callback after the flip transition.
	// page is the current item's index.
	// isLimit is true if the current page is the last one (or the first one).
	onEndFlip   : function( page, isLimit ) { return false; },
	 
	// callback before the flip transition.
	// page is the current item's index.
	onBeforeFlip: function( page ) { return false; }
	
在綁定下一頁和上一頁的事件裡面，除了可以直接在**bookblock()**添加以外

	$( '#bb-bookblock' ).bookblock( {
		speed				: 800,
		shadowSides	: 0.8,
		shadowFlip	: 0.7,
		nextEl      : '#bb-nav-next', //綁定下一頁事件
		prevEl      : '#bb-nav-prev'  //綁定上一頁事件
	} )
	
也可以按照範例裡面的寫法

	var config = {
		$bookBlock: $( '#bb-bookblock' ),
		$navNext	: $( '#bb-nav-next' ),
		$navPrev	: $( '#bb-nav-prev' ),
		$navJump	: $( '#bb-nav-jump' ),
		bb				: $( '#bb-bookblock' ).bookblock( {
			speed				: 800,
			shadowSides	: 0.8,
			shadowFlip	: 0.7
		} )
	}
	
	config.$navNext.on( 'click', function() {

		config.bb.next();
		return false;

	} );

	config.$navPrev.on( 'click', function() {
		
		config.bb.prev();
		return false;

	} );
	
另外自己綁定click在上一頁和下一頁的DOM元素裡面

範例完成以後我特地拿iPone來測試swipe even的效果，還蠻頓的，而且不是很靈敏，可能有細節要再調整，也有可能是手機本身的問題，這方面就要請各位要應用在行動裝置的朋友們再多多測試了

參考資料:

<a href="http://modernizr.com/docs/#features-css" target="_blank">Modernizr Documentation</a>

如有錯誤，歡迎指正