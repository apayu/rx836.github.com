---
layout: post
title: "[jQuery] hoverpulse 滑鼠移入，圖片縮放"
date: 2012-09-20 23:42
comments: true
categories: 
---

jQuery寫了一陣子，直到最近有個需求，想要做到滑鼠移到圖片上，會微微的放大，才發現這個很常看到的效果，我到今天都還沒實做過

<!--more-->

幸運的是...，就因為這麼晚才實做，所以早就有人把plugin寫好了，我所用的是<a href="http://www.malsup.com/jquery/hoverpulse/" target="_blank">hoverpulse</a>，用法相當相當的簡單

首先是HTML部份

	<div><img src="a.jpg" /></div>
	<div><img src="b.jpg" /></div>
	<div><img src="c.jpg" /></div>
	
再來是jQuery部份

	$(document).ready(function() {
		$('div img').hoverpulse();
	});
	
這樣就完成了！當然什麼值都沒有給的情況下是用default，但如果想要設定放大的幅度和變化的速度，可以這樣寫

	$(document).ready(function() {
		$('div img').hoverpulse({
			size: 40,  // number of pixels to pulse element (in each direction)
			speed: 400 // speed of the animation 
		});
	});
	
真的簡單又明瞭...

那如果你想加入點擊的事件，你可以這樣寫

	$(document).ready(function() {
		$('div img').hoverpulse().each(function() {
			var $img = $(this);					
			$img.click(function() {
				
				//點每張圖的事件
				
				return false;
			});
		});
	});

接下來是我個人好奇去看他的source code，可以看到他先將每個圖片的width和height存到$.data裡面

	this.each(function() {
		var $this = $(this);
		var w = $this.width(), h = $this.height();
		$this.data('hoverpulse.size', { w: parseInt(w), h: parseInt(h) });
	});
	
接著利用到**.hover()**的方法去做出滑鼠移到圖片和移出圖片的效果

	// bind hover event for behavior
	return this.hover(
		// hover over
		function() {
			var $this = $(this);
			$this.parent().css('z-index', opts.zIndexActive);
			
			var size = $this.data('hoverpulse.size');
			var w = size.w, h = size.h;
			$this.stop().animate({ 
				top:  ('-'+opts.size+'px'), 
				left: ('-'+opts.size+'px'), 
				height: (h+2*opts.size)+'px', 
				width:	(w+2*opts.size)+'px' 
			}, opts.speed);
		},
		// hover out
		function() {
			var $this = $(this);
			var size = $this.data('hoverpulse.size');
			var w = size.w, h = size.h;
			
			$this.stop().animate({ 
				top:  0, 
				left: 0, 
				height: (h+'px'), 
				width:	(w+'px') 
			}, opts.speed, function() {
				$this.parent().css('z-index', opts.zIndexNormal);
			});
		}
	);
	
在移入部份會先將包覆img的div z-index值設到100

	$this.parent().css('z-index', opts.zIndexActive);
	
然後從data取出之前放入的圖片width和height，接著用**.animate()**來執行放大效果

	$this.stop().animate({ 
				top:  ('-'+opts.size+'px'), 
				left: ('-'+opts.size+'px'), 
				height: (h+2*opts.size)+'px', 
				width:	(w+2*opts.size)+'px' 
			}, opts.speed);
			
這段code其實就是把你設定的size放大兩倍，並且為了有感覺從圖片中間點開始放大的效果，所以把位置top和left給予負值，等於整張圖片往左上角移動，速度是**opts.speed**，而圖片的position:absolute在整個plugin一開始就已經設定了

	// parent must be relatively positioned
	this.parent().css({ position: 'relative' });
	// pulsing element must be absolutely positioned
	this.css({ position: 'absolute', top: 0, left: 0 });
	
可以看到包覆img的div是relatively，img是absolute

而滑鼠移開之後只是把值恢復成原來的設定

	var $this = $(this);
	var size = $this.data('hoverpulse.size');
	var w = size.w, h = size.h;
	
	$this.stop().animate({ 
		top:  0, 
		left: 0, 
		height: (h+'px'), 
		width:	(w+'px') 
	}, opts.speed, function() {
		$this.parent().css('z-index', opts.zIndexNormal);
	});
	
將top和left歸為0，height和width恢復成原來的大小，z-index也設回預設值1

當然預設值在plugin的最下面可以自己修改

	$.fn.hoverpulse.defaults = {
		size:  20,
		speed: 200,
		zIndexActive: 100,
		zIndexNormal: 1
	};

這樣plugin整個看起來就很清楚明瞭，也可以自己嘗試動手寫寫看喔！

## 後記

Aaron大大說plugin寫法有點舊，而且有點囉嗦XD，他建議我新的寫法，在此特別筆記下來

HTML

	<img src="a.jpg" class="resize" width="250"/>
	
jQuery
	
	var current_h = null;
	var current_w = null;

	$('.resize').hover(
		function(){
			current_h = $(this, 'img').height;
			current_w = $(this, 'img').width;
			$(this).stop(true, false).animate({width: (current_w * 1.3), height: (current_h * 1.3)}, 300);
		},
		function(){
			$(this).stop(true, false).animate({width: current_w + 'px', height: current_h + 'px'}, 300);
		}
	);
	
不要用plugin，直接寫，至於top和left在自己加上就好，跟前面的plugin道理一樣

參考資料:

<a href="http://www.malsup.com/jquery/hoverpulse/" target="_blank">hoverpulse</a>

如有錯誤，歡迎指正