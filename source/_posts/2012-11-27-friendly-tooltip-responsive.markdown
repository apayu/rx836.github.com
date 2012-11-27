---
layout: post
title: "[jQuery] 自製擁有Responsive的Tooltip"
date: 2012-11-27 11:53
comments: true
categories: jQuery CSS
---

<img src="https://lh6.googleusercontent.com/-KiD_TaOPzFA/ULRxljbyVVI/AAAAAAAAB-M/nHY1WuJDaGE/s373/q1.jpg" />

之前做Tooltip，都是上網找plugin比較多，但這次看到一篇文章，是自己寫一個Tooltip，就來記錄一下，而且還有Responsive的效果，可以依照載具大小做縮放和位置的改變，code不多，也很簡單明瞭

<!--more-->

先稍微介紹一下什麼是Tooltip，就如上面的圖所示，他可以提供良好的 **user experience**，可以在某個功能或選單，又或是某段文字上，在滑鼠移過去時(有時候是在點擊情況下，但少數)，出現一個小框，裡面有少許的說明文字，讓用戶知道，這個功能或是按鈕是在幹嘛

首先，是CSS的部分

	#tooltip
	{
		text-align: center;
		color: #fff;
		background: #111;
		position: absolute;
		z-index: 100;
		padding: 15px;
	}
	 
		#tooltip:after /* triangle decoration */
		{
			width: 0;
			height: 0;
			border-left: 10px solid transparent;
			border-right: 10px solid transparent;
			border-top: 10px solid #111;
			content: '';
			position: absolute;
			left: 50%;
			bottom: -10px;
			margin-left: -10px;
		}
	 
			#tooltip.top:after
			{
				border-top-color: transparent;
				border-bottom: 10px solid #111;
				top: -20px;
				bottom: auto;
			}
	 
			#tooltip.left:after
			{
				left: 10px;
				margin: 0;
			}
	 
			#tooltip.right:after
			{
				right: 10px;
				left: auto;
				margin: 0;
			}
			
這段CSS是建立一個tooltip，包括在不同載具時，呈現tooltip在不同的適當位置(bottom、top、left、right)，不過這邊有個小技巧要特別拿出來說明一下

就是Tooltip上面那個小箭頭其實是用CSS畫出來的

<img src="https://lh4.googleusercontent.com/-jhfjv_hv-hY/ULRzfM9ycJI/AAAAAAAAB-w/oOohCQO9N6w/s373/q6.jpg" />

不同的CSS畫法，可以參考下面範例，HTML部分就只要一個div

###用CSS畫出三角型

<img src="https://lh3.googleusercontent.com/-kNDtVnCgUzE/ULRxloJG7qI/AAAAAAAAB-U/Jkfm3E0DC6k/s112/q2.jpg" />
	
	div {
		width: 0;
		height: 0;
		border-left: 50px solid #fff;
		border-right: 50px solid #fff;
		border-bottom: 100px solid black;
	}
	
<img src="https://lh5.googleusercontent.com/-siEgv7d8AJM/ULRxmDlFMeI/AAAAAAAAB-Q/BFmufqFJ3VU/s115/q4.jpg" />
	
	div {
		width: 0;
		height: 0;
		border-top: 50px solid #fff;
		border-right: 100px solid black;
		border-bottom: 50px solid #fff;
	}
	
<img src="https://lh6.googleusercontent.com/-VWF99ZiXIo8/ULRxlgGjbuI/AAAAAAAAB-I/ASZmQTUURI4/s110/q3.jpg" />
	
	div {
		width: 0;
		height: 0;
		border-left: 50px solid #fff;
		border-right: 50px solid #fff;
		border-top: 100px solid black;
	}
	
<img src="https://lh4.googleusercontent.com/-bjaIIy9c9Ow/ULRxmXa20iI/AAAAAAAAB-Y/ZvF6cRBvc1I/s107/q5.jpg" />
	
	div {
		width: 0;
		height: 0;
		border-top: 50px solid #fff;
		border-right: 100px solid black;
		border-bottom: 50px solid #fff;
	}

當然如果希望是別的底色可以自己再做修改，接下來是JS部分

	$( document ).ready( function()
	{
		var targets = $( '[rel~=tooltip]' ),
			target  = false,
			tooltip = false,
			title   = false;
	 
		targets.bind( 'mouseenter', function()
		{
			target  = $( this );
			tip     = target.attr( 'title' );
			tooltip = $( '<div id="tooltip"></div>' );
	 
			if( !tip || tip == '' )
				return false;
	 
			target.removeAttr( 'title' );
			tooltip.css( 'opacity', 0 )
				   .html( tip )
				   .appendTo( 'body' );
	 
			var init_tooltip = function()
			{
				if( $( window ).width() < tooltip.outerWidth() * 1.5 )
					tooltip.css( 'max-width', $( window ).width() / 2 );
				else
					tooltip.css( 'max-width', 340 );
	 
				var pos_left = target.offset().left + ( target.outerWidth() / 2 ) - ( tooltip.outerWidth() / 2 ),
					pos_top  = target.offset().top - tooltip.outerHeight() - 20;
	 
				if( pos_left < 0 )
				{
					pos_left = target.offset().left + target.outerWidth() / 2 - 20;
					tooltip.addClass( 'left' );
				}
				else
					tooltip.removeClass( 'left' );
	 
				if( pos_left + tooltip.outerWidth() > $( window ).width() )
				{
					pos_left = target.offset().left - tooltip.outerWidth() + target.outerWidth() / 2 + 20;
					tooltip.addClass( 'right' );
				}
				else
					tooltip.removeClass( 'right' );
	 
				if( pos_top < 0 )
				{
					var pos_top  = target.offset().top + target.outerHeight();
					tooltip.addClass( 'top' );
				}
				else
					tooltip.removeClass( 'top' );
	 
				tooltip.css( { left: pos_left, top: pos_top } )
					   .animate( { top: '+=10', opacity: 1 }, 50 );
			};
	 
			init_tooltip();
			$( window ).resize( init_tooltip );
	 
			var remove_tooltip = function()
			{
				tooltip.animate( { top: '-=10', opacity: 0 }, 50, function()
				{
					$( this ).remove();
				});
	 
				target.attr( 'title', tip );
			};
	 
			target.bind( 'mouseleave', remove_tooltip );
			tooltip.bind( 'click', remove_tooltip );
		});
	});

JS部分，就是當「mouseenter」的事件發生時，加上id為tooltip的div，「mouseleave」時就把div也就是tooltip移除

「init_tooltip」主要是計算載具視窗的大小，來給予tooltip相對的位置和添加類別，其中說明一下 **.outerWidth()** 這個方法
<br/>
<br/>
###width()、innerWidth()、outerWidth()的三者差別
**width()**: 一般我們取得一個元素的寬都會用，取出來的值只有<span style="color:red">宽度</span>

**innerWidth()**: <span style="color:red">宽度</span>+<span style="color:red">內距(padding)</span>

**outerWidth()**: <span style="color:red">宽度</span>+<span style="color:red">內距(padding)</span>+<span style="color:red">邊框(boder)</span>

**outerWidth(true)**: 如果給true的話(預設是false)，<span style="color:red">宽度</span>+<span style="color:red">內距(padding)</span>+<span style="color:red">邊框(boder)</span>+<span style="color:red">邊界(margin)</span>
<br/>
<br/>
這樣，搭配幾個小技巧，一個簡單又好用的Tooltip就可以自己製作，而不用再去找相關的plugin

參考資料:

<a href="http://osvaldas.info/elegant-css-and-jquery-tooltip-responsive-mobile-friendly" target="_blank">Responsive and Mobile-Friendly Tooltip</a>

<a href="http://osvaldas.info/examples/elegant-css-and-jquery-tooltip-responsive-mobile-friendly/" target="_blank">Demo</a>

<a href="http://wyz.67ge.com/css-triangle/" target="_blank">使用纯CSS实现的各种三角，全浏览器兼容</a>

<a href="http://www.dearoom.com/blog/jquery%E4%B8%AD-heightwidth-innerheightinnerwidth-outerheightouterwidth%E7%9A%84%E5%8C%BA%E5%88%AB/" target="_blank">jQuery中 height(width) innerHeight(innerWidth) outerHeight(outerWidth)的区别</a>

內容如有錯誤，歡迎指正

