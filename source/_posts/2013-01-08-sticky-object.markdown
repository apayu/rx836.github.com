---
layout: post
title: "[jQ-Plugin] 跟著Pinterest將menu固定起來 - Sticky"
date: 2013-01-08 11:11
comments: true
categories: jQ-Plugin
---

pinterest的網站設計影響了許多人，之前也曾經寫過實做的文章 - <a href="http://blog.rx836.tw/blog/jquery-waterfall-infinitescroll/" target="_blank">做出Pinterest效果的介面 用jQuery Masonry + Infinite Scroll</a>，但其實在這種被稱為 Waterfall 的網頁設計底下，還有許多小技巧和應用需要學習

<!--more-->

其中一個就是將上方的 menu 固定在整個視窗的某個地方，因為像這種無限延伸的設計，不知道整個網頁會長到多長，在User瀏覽網頁時，如果想要中途切換其他頁面，沒有將 menu 固定在視窗的某個區塊，會發現拉回最上方非常的不方便，所以一般來說都會設計成跟著頁面做移動，如下圖

一開始menu固定在上方的某個區塊

<img src="https://lh3.googleusercontent.com/-QU3DxU6ccVg/UOu9t-bGOmI/AAAAAAAACKY/y8rQuxSivyA/s671/2013-01-08_114010.jpg" />

當頁面往下拉時，會跟著移動

<img src="https://lh5.googleusercontent.com/-A57qEkc8I7s/UOu9tzDm2FI/AAAAAAAACKc/ALiiUe-IdrQ/s589/2013-01-08_114044.jpg" />

要實現這樣的設計並不困難，今天就來介紹一款方便的jQuery plugin - Sticky

##Start

首先先從github下載js檔回來

<a href="https://github.com/garand/sticky" target="_blank">DOWNLOAD PLUGIN</a>

裡面有個檔名為jquery.sticky.js，將他載入到網頁裡面

接著html部份

	<p>上方元素</p>
	<div id="sticker">
		<p>我是menu</p>
	</div>
	<p>下方元素</p>
	
id為 sticker 的&lt;div&gt;就是要被固定在上方的元素，為了方便demo，可以給他一些css樣式

	body {
      height: 10000px;
      padding: 0;
      margin: 0;
    }

    #sticker {
      background: #bada55;
      color: white;
      width: 300px;
      font-family: Droid Sans;
      font-size: 40px;
      line-height: 1.6em;
      font-weight: bold;
      text-align: center;
      padding: 20px;
      margin: 0 auto;
      text-shadow: 0 1px 1px rgba(0,0,0,.2);
      border-radius: 50px;
    }
	
這邊注意到 body 的 height 為1000px是為了讓網頁可以一直往下拉

接著是js部份

	$("#sticker").sticky({ topSpacing: 0, center:true, className:"hey" });
	
最後來看展示結果

捲動網頁前

<img src="https://lh3.googleusercontent.com/-xma-MsT9Zww/UOu9t_QwQGI/AAAAAAAACKU/cdJD0qMOFNM/s1023/2013-01-08_124326.jpg" />

捲動網頁後

<img src="https://lh4.googleusercontent.com/-NJLAKGJfXP0/UOu9u6udgXI/AAAAAAAACKg/VISQuhKeefM/s1003/2013-01-08_124342.jpg" />

會發現 "我是menu" 這個區塊會一直固定在網頁上方，達到我們想要的效果，如果圖片說明不清，建議還是實做 Demo 比較清楚XD

##參數部份

topSpacing: 元素與頁面頂端有多少固定距離

bottomSpacing: 元素與頁面底端有多少固定距離

className: 當觸發事件時增加的 CSS class, 預設是is-sticky

wrapperClassName: 自訂 wrapper CSS class, 預設是sticky-wrapper

getWidthFrom: 選擇一個元素做為參考值設定為固定寬度

##想要自己實做的話..

如果試著去看 source code 的話，會發現實做並不困難，主要就是計算 **scrollTop()** 目前的位置，如果大於某個值就觸發事件，將要固定的元素添加 position:fixed，接著在看要距離上方多少空間就設定多少 top 值，主要的判斷程式碼部分如下，有興趣的人可以再自行參考


	if (scrollTop <= etse) {
	  if (s.currentTop !== null) {
		s.stickyElement
		  .css('position', '')
		  .css('top', '');
		s.stickyElement.parent().removeClass(s.className);
		s.currentTop = null;
	  }
	}
	else {
	  var newTop = documentHeight - s.stickyElement.outerHeight()
		- s.topSpacing - s.bottomSpacing - scrollTop - extra;
	  if (newTop < 0) {
		newTop = newTop + s.topSpacing;
	  } else {
		newTop = s.topSpacing;
	  }
	  if (s.currentTop != newTop) {
		s.stickyElement
		  .css('position', 'fixed')
		  .css('top', newTop);

		if (typeof s.getWidthFrom !== 'undefined') {
		  s.stickyElement.css('width', $(s.getWidthFrom).width());
		}

		s.stickyElement.parent().addClass(s.className);
		s.currentTop = newTop;
	  }
	}

###參考資料:

<a href="http://stickyjs.com/" target="_blank">Sticky</a>

內容如有錯誤，歡迎指正

