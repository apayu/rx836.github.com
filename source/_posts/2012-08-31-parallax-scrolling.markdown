---
layout: post
title: "[jQuery] jQuery scroll parallax plugin"
date: 2012-08-31 17:55
comments: true
categories: jQuery
---

在Facebook看到有人分享<a href="http://www.milwaukeepolicenews.com/#menu=home-page" target="_blank">這個網站</a>，有人提到是用parallax scroll來實做，因為對這個不熟悉，所以趕緊做了一些功課來看看怎麼做

<!--more-->

parallax scroll中文叫做**視差滾動效果**，意思就是指讓多層背景以不同的速度移動，形成立體的景深效果，使User有豐富的視覺體驗，像<a href="http://www.nikebetterworld.com/" target="_blank">Nike</a>一直對這方面運用的相當好，還有<a href="http://www.hksilicon.com/kb/articles/57516/30Parallax-Scrolling" target="_blank">『30個讓人興奮的視差滾動（Parallax Scrolling）效果網站』</a>也收集了很多相關方面的網站

為了能夠實做，找到了<a href="http://www.davecranwell.com/content/jquery-scroll-parallax-plugin" target="_blank">JQUERY SCROLL PARALLAX</a>這個plugin，用法蠻簡單的，首先準備ab兩張圖，a圖長方形(例如200x2000)，顏色隨意，b圖正方形(例如100x100)，顏色隨意，注意不要跟a圖一樣就可以，方便辨識

接著HTML如下:

	<div class="item">
		<div class="inner"></div>		
	</div>
	
CSS如下:

	.item{
		width:100%;
		overflow:hidden;
		position:relative;
		height:2000px;
		background: white url(a.png) 0px 0px fixed no-repeat;
	}
	
	.inner{
		width:100%;
		height:100%;
		position:absolute;
		z-index:1;
		background: url(b.png) 150px 200px fixed no-repeat;
	}
	
會看到我將.inner的背景圖設置了座標150,200，200就是等會js負責控制的地方，經由控制背景圖的位置來達到視差滾輪的效果

接著引用js

	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.8.0/jquery.min.js"></script>	
	<script src="jquery.inview.js"></script>
	<script src="jquery.scrollParallax.js"></script>
	
共有兩個js要載，一個就是<a href="https://github.com/davecranwell/jQuery-scroll-parallax" target="_blank">scrollParallax.js</a>，另一個是<a href="https://github.com/protonet/jquery.inview" target="_blank">inview.js</a>，inview.js簡單的說也是一個plugin，藉由inview.js可以抓取目前scroll的位置和秀出對應的效果，例如『把scroll拉到最底就出現回到最上方的方塊』

接著是js程式碼部分

	$(function(){		
		$('.item').scrollParallax({
			'speed': 0
		});
				
		$('.item .inner').scrollParallax({
			'speed': 0.8		
		});
	});
	
speed是調整移動的數度，只要將每個圖速度設定不一樣，就會呈現不一樣的景深效果

很容易吧！有興趣的人可以下載試試看，而且都有DEMO範例，方便理解

如有錯誤，歡迎指證

參考資料:

<a href="http://www.davecranwell.com/content/jquery-scroll-parallax-plugin" target="_blank">JQUERY SCROLL PARALLAX PLUGIN</a>