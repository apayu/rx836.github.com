---
layout: post
title: "[CSS] 用CSS改變scrollbar"
date: 2013-01-04 11:03
comments: true
categories: CSS
---

<img src="https://lh6.googleusercontent.com/-STc4lvK5aJw/UOZ8yP4FfFI/AAAAAAAACIo/oscopBlrZ7k/s202/2013-01-04_110558.jpg" />

scrollbar在網頁裡面算是相當常見的元素，因為資訊爆炸，每個網頁都有許多豐富的內容，為了減少分頁，往往會進而拉長整個網頁的長度，這時候就會產生scrollbar，但原生的 scrollbar 有時候跟網頁的整體UI設計並不符合，看起來就很突兀，為了讓網站整體的UI設計一致，我們可以嘗試改變一下 scrollbar 的樣式

<!--more-->

##準備一個簡單的 scrollbar 頁面

首先在開始改變 scrollbar 之前，我們必須先知道哪些情境之下會出現scrollbar

1.當網頁內容長度超過瀏覽器視窗的可視範圍時，會在右側出現scrollbar

2.當 textarea 包含足夠的文字時

3.利用 iframe 顯示不同頁面時

4.&lt;div&gt;或其他 block element 有設置 overflow 屬性時

現在我們選擇用第四種設置&lt;div&gt;的屬性 overflow 來當作 demo 練習

html

	<div class="container">
		<p>這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文</p>
		<p>這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文</p>
		<p>這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文</p>
		<p>這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文</p>dit. In ultrices vehicula pretium.</p>
		<p>這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文</p>
		<p>這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文這是一段假文</p>
	</div>

css

	.container {
		  width: 400px;
		  height: 300px;
		  background-color: #DCDCDC;
		  overflow: scroll; /* showing scrollbars */
	}

CSS部份我們替&lt;div&gt;設置了 width 和 height，目的是為了讓內容限制一個範圍，那當超出範圍的部份，我們就設置了另一個屬性 **overflow:scroll**，告訴瀏覽器做 scrollbar 的處理，所以設置完的顯示結果如下

<img src="https://lh4.googleusercontent.com/-yinWVlS8WjI/UOZ8yc9bwmI/AAAAAAAACIs/axfVRTRAXK0/s418/2013-01-04_115358.jpg" />

##Webkit瀏覽器的scrollbar

假設是 Webkit 的瀏覽器(例如: Google Chrome、Apple Safari)，我們可以使用 ::-webkit-scrollbar 這個 pseudo-elements 來做改變

	::-webkit-scrollbar {
		  width: 50px;
	}
	::-webkit-scrollbar-track {
		  background-color: red;
	} 
	::-webkit-scrollbar-thumb {
		  background-color: blue
	}
	::-webkit-scrollbar-button {
		  background-color: yellow
	}
	::-webkit-scrollbar-corner {
		  background-color: black;
	}
	
顯示效果如下

<img src="https://lh4.googleusercontent.com/-GjRmeALubYA/UOZ8yfCuvaI/AAAAAAAACIw/XuFAQAPU8AM/s419/2013-01-04_122330.jpg" />

很醜，但為了讓大家知道每個屬性的效果，所以特地用顏色做區別，還把寬度設為50px，但現實的專案中千萬別這樣做，還是要像前面所說的，要符合整體的網站UI設計才行

不過以上的寫法只適用於 Webkit browsers

##IE呢？

其實沒查可能還不知道，IE是第一個支援用CSS來改變 scrollbar 樣式的瀏覽器，早在IE5.5就可以實做，不過僅限於顏色的改變

用我們剛剛的範例當例子，我們可以這樣寫

	body {
		scrollbar-face-color: #b46868;
	}

結果如下

<img src="https://lh6.googleusercontent.com/-Rqkd_jSbObM/UOZ8y042JnI/AAAAAAAACI0/SHLaovEZDS8/s420/2013-01-04_123209.jpg" />

##jScrollPane

剛剛只談到 Webkit 的瀏覽器還有IE的寫法，那Firefox怎麼辦呢？有沒有比較方便的方法可以適用於大多數的瀏覽器，其實是有的，可以嘗試 <a href="http://jscrollpane.kelvinluck.com/" target="_blank">jScrollPane</a> 這個jQuery plugin

基本的使用方式如下，在網頁裡面載入jQuery和jquery.jscrollpane.min.js還有jquery.jscrollpane.css

	<script type="text/javascript" src="http://code.jquery.com/jquery-1.8.2.js"></script>
	<script type="text/javascript" src="jquery.jscrollpane.min.js"></script>
	<link rel="stylesheet" type="text/css" href="jquery.jscrollpane.css" />
	
接著是js部份

	$('.container').jScrollPane();
	
效果如下

<img src="https://lh5.googleusercontent.com/-LkkEeHILftE/UOZ8zOOTPII/AAAAAAAACI8/B4y_gaz4-Dw/s414/2013-01-04_124917.jpg" />

如果要修改樣式的話，可以直接修改jquery.jscrollpane.css這支檔案裡面的幾個類別屬性

	.jspTrack
	{
		background: #dde; //可以更改顏色
		position: relative;
	}

	.jspDrag
	{
		background: #bbd; //可以更改顏色
		position: relative;
		top: 0;
		left: 0;
		cursor: pointer;
	}

或許會有疑問，為什麼用 jScrollPane 可以支援不同的瀏覽器？其實只要打開 firebug 看看HTML的部份就可以知道

<img src="https://lh4.googleusercontent.com/-UNhAOrBS60U/UOZ80MiprjI/AAAAAAAACJM/ClXt8YzMY-Q/s420/2013-01-04_144723.jpg" />

原來 jScrollPane 是用&lt;div&gt;做出假的 scrollbar，至於位移的效果就是改變CSS屬性top的值
	
##結論

修改 scrollbar 在許多Web Apps都可以看的到實做，像微軟的 Outlook 信箱服務

<img src="https://lh5.googleusercontent.com/-PAU7cSx0tIQ/UOZ8zRWFhII/AAAAAAAACJI/PDzHVetCHv0/s486/2013-01-04_144215.jpg" />

又或是Google的雲端硬碟服務

<img src="https://lh4.googleusercontent.com/-OHN4PIVruTQ/UOZ8zg-ErCI/AAAAAAAACJA/Q8WkMSdEt0o/s454/2013-01-04_144319.jpg" />

都有畫龍點睛的效果，善用這方面的方法，可以讓網站的UI看起來更一致，也不必局限於原生HTML元素的呈現，網頁也可以更加活潑

###參考資料:

<a href="phttp://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/quick-tip-styling-scrollbars-to-match-your-ui-design/?utm_source=CSS+Weekly&utm_campaign=CSS_Weekly_Issue_34&utm_medium=web" target="_blank">Quick Tip: Styling Scrollbars to Match Your UI Design</a>

內容如有錯誤，歡迎指正
	
	
