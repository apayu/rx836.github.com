---
layout: post
title: "[jQ-Plugin] 做出磁磚效果變化的圖片轉換"
date: 2013-01-18 16:36
comments: true
categories: jQ-Plugin
---
<img src="https://lh4.googleusercontent.com/-WH3Ni1ou3Ww/UPkk71vSTvI/AAAAAAAACMk/hcFofq9eTuU/s641/2013-01-18_164425.jpg" />

不知道大家有沒有看過這種切成一塊一塊的轉換圖片，類似磁磚拼貼的效果，最近看到一篇講解教學的文章，自己消化了一下，來分享並且紀錄下來

<!--more-->

##Start

首先是HTML部份

	<div class="sliced">
		<img src="pic.jpg"/>
	</div>
	
只用一個&lt;div&gt;包住一個&lt;img&gt;

接著是CSS

	.sliced {
		position: relative;
		width: 640px; 
		height: 400px;
	}
	
因為我們要將效果自製成一個jQuery plugin，方便以後可以重複使用，所以這邊要先建立一個基本的 jQuery plugin 樣板

	;(function( $, window ) {
	 
		//預設值
		var _defaults = {
			x      : 2, // 預設對圖片x軸要切幾塊
			y      : 2, // 預設對圖片y軸要切幾塊
			random : true, // 磚塊是否要按照順序切換
			speed  : 2000 // 效果的速度
		};				

		$.fn.sliced = function( options ) {

			var o = $.extend( {}, _defaults, options );

			return this.each(function() {
				var $container = $(this); // cache selector for best performance
				// 主要程式碼從這裡開始寫			
				
			});
		};
	 
	}( jQuery, window ));
	
當然如果想要寫其他 Plugin 的人，也可以使用這個樣板去做修改

###原理

做好基本的準備工作以後，我們要來開始撰寫主程式部分，但在撰寫之前，先來說明一下這個效果是如何產生，其實原理很簡單，在效果執行時，會先將原圖的屬性設為 **display: none**，接著加上&lt;div&gt;並且設定背景圖片，類似拼圖一樣一塊一塊拼出原圖，如果覺得我描述的不清楚的話，下面有範例可以參考XD

<a href="http://jsfiddle.net/rx836/sbBeA/" target="_blank">範例</a>

這邊的重點在於 **background-position** 這個屬性，利用這個屬性做背景圖片的位移，每一個&lt;div&gt;代表著圖片的一個區塊，也許有些人看到這邊已經知道端倪，因為只要把圖片轉換成一個一個的&lt;div&gt;，透過操作每個&lt;div&gt;，就可以做出特效

接著我們把程式碼寫完，先建立一些變數

	var width = $container.width(),
		height = $container.height(),
		$img = $container.find('img'),
		n_tiles = o.x * o.y,
		tiles = [], $tiles;
		
接著是建立一塊一塊的磁磚，並且把原圖隱藏，最後加上剛建立好的磁磚，至於要建立多少個就看當初給予的值
		
	for ( var i = 0; i < n_tiles; i++ ) {
		tiles.push('<div class="tile"/>');
	}

	$tiles = $( tiles.join('') );

	//將原圖隱藏並加上磁磚
	$img.hide().after( $tiles );

接著利用原始圖檔當作每個磁磚的背景圖，在將背景圖做適當的位移，至於要位移多少，就看每個&lt;div&gt;(也就是每個磁磚)所代表的區塊
	
	//利用原始圖檔當作磁磚背景圖
	$tiles.css({
		width: width / o.x,
		height: height / o.y,
		backgroundImage: 'url('+ $img.attr('src') +')'
	});    

	//替背景圖調整位置
	$tiles.each(function() {
		var pos = $(this).position();
		console.log(pos);
		$(this).css( 'backgroundPosition', -pos.left +'px '+ -pos.top +'px' );
	});
	
因為要拼成一塊圖片的關係，所以也要利用 float這個屬性，直接在CSS加上即可

	.tile { float: left; }
	
到這邊為止，你可以加上下面這段程式碼，看看效果如何

	$('.sliced').sliced({ x:4, y:4 }); // 將圖片切成4x4
	
看圖片好像沒什麼改變，但打開firebug看看HTML部份，有發現到不一樣了嗎？

<img src="https://lh5.googleusercontent.com/-t0N7b55zbPE/UPkk8Kc6OaI/AAAAAAAACMo/1L6StJdwJ3s/s1026/2013-01-18_180320.jpg" />

就如剛剛所敘述的，**原始圖片已經隱藏，並且用&lt;div&gt;拼湊而出**

###製作效果

知道了原理以後，接著讓我們繼續把程式碼繼續寫完，接下來是隨機變換的部份


	function range( min, max, rand ) {
	  var arr = ( new Array( ++max - min ) )
		.join('.').split('.')
		.map(function( v,i ){ return min + i });
	  return rand
		? arr.map(function( v ) { return [ Math.random(), v ] })
		   .sort().map(function( v ) { return v[ 1 ] })
		: arr;
	}
	
這部份的 code 可以參考 <a href="http://stackoverflow.com/questions/12528886/random-but-just-in-chrome" target="_blank">stackoverflow</a>，簡單來說就是一個產生**特定範圍的隨機排列的數字**，但因為是函式的關係我們要把他跟一開始**建立預設值 var _defaults 放在一起**，剩下的 code 就是處理切換效果的部份

	var tilesArr = range( 0, n_tiles, o.random ),
	tileSpeed = o.speed / n_tiles;				
	
	$container.on( 'animate', function() {

		tilesArr.forEach(function( tile, i ) {					
			setTimeout(function(){
				$tiles.eq( tile ).toggleClass( 'tile-animated' );
			}, i * tileSpeed );
		});

	});

我們將每個磁磚加上animate，在特定時間內做 opacity 屬性的變化，最後加上一個按鈕做觸發，和套用plugin，看看效果如何

html

	<button>Toggle</button>

js

	$('button').click(function() {
		$('.sliced').trigger('animate');
	});
	
<a href="http://jsfiddle.net/rx836/jQaJh/2/" target="_blank">完整的範例</a>

##結論

只要知道是拼圖的概念，就可以知道其實不是針對原圖去做變化，巧妙的利用&lt;div&gt;也可以做出類似flash的效果

###參考資料:

<a href="http://www.onextrapixel.com/2012/11/23/how-to-slice-images-into-tiles-with-jquery-and-css3-transitions/" target="_blank">How to Slice Images into Tiles with jQuery and CSS3 Transitions</a>

內容如有錯誤，歡迎指正

