---
layout: post
title: "[CSS] 利用CSS3做scrolling effect"
date: 2012-12-11 07:05
comments: true
categories: CSS
---

<img src="https://lh6.googleusercontent.com/-URpPFCw8GZY/UMZ5NsXYJuI/AAAAAAAACC4/Bjab2PYz86w/s1077/2012-12-11_071208.jpg" />

今天看到一篇文章介紹美國 <a href="http://www.ebay.com/new" target="_blank">ebay</a> 網站的scrolling effect，觀念其實蠻簡單的，重點是我原本以為需要用到js才能達到，但後來發現根本連一行js都不用寫，只需要用到CSS3即可，這邊就來筆記一下過程

<!--more-->

##Start

一開始先準備三張可以延伸到整個螢幕大小的照片，如果手邊沒有，可以直接使用文章裡面的<a href="pepsized.com/wp-content/uploads/2012/11/lavender.zip" target="_blank">Demo</a>，就有現成的圖片可以練習，另外下面都是用Demo裡面的檔案做講解

HTML部份

	<!DOCTYPE html>
	<html class="no-js" lang="en">
	<head>
	<meta charset="utf-8">
	<title>From love for lavender</title>
	<!-- 略... -->
	</head>
	<body>
	<header class=" content">
			<div class="wrapper">
					<h1>From love for lavender</h1>
					<p><span>Lavender</span> (botanic name Lavandula) is a ....
					</p>
			</div>
	</header>

	<section class="content" id="oil">
			<div class="wrapper">
					<p><span>Lavender oil</span> is an ... </p>
			</div>
	</section>
	<!-- 略... -->
	<footer>
			<div class=wrapper>
					 "From love for lavender" has been built ...
			</div>
	</footer>
	</body>
	</html>
	
HTML部份就是常見的HTML5的架構，有&lt;header&gt;、&lt;section&gt;和&lt;footer&gt;，每個裡面都包含有一個class為 "wrapper" 的&lt;div&gt;

再來是基本的CSS部份

	.wrapper {
		width: 100%;
		margin: 0 auto;
		-webkit-box-sizing: border-box;
		-moz-box-sizing: border-box;
		box-sizing: border-box; 
	}
	
會看到有一個比較少見的屬性叫 **box-sizing**，他是CSS3的屬性，如果我們設box-sizing為 **border-box**，意思就是指width和height的部份都包含了 **padding** 和 **border**，詳細的屬性說明可以參考 <a href="http://www.w3cplus.com/content/css3-box-sizing" target="_blank">這篇</a>

接著是scrolling effect部份

	section:after, header:after {
		content: "";
		display: block;
		height: 400px;
		width: 100%;
		background-size: cover;
		background-position: center center;
		background-repeat: no-repeat;
		background-attachment: fixed;
		box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.6); 
	}
	
	header:after {
	  background-image: url(../images/lavenderbg1.jpg); }
	#oil:after {
	  background-image: url(../images/lavenderbg2.jpg); }
	#culinary:after {
	  background-image: url(../images/lavenderbg3.jpg); }
	#dried:after {
	  background-image: url(../images/lavenderbg4.jpg); }
	
因為沒有用到js的關係，但我們又想在HTML上新增元素，所以我們可以利用CSS的pseudo-elements **:after**，他會幫我們在元素後面加上新的元素上去，並且擁有 **background**，另外，我們將屬性 **background-attachment** 設定為fixed，這也是scrolling effect的重點所在，意思就是指**當頁面滾動時，背景圖並不會跟著移動**

這樣就大功告成囉，有沒有覺得效果很不錯呢？

###參考資料:

<a href="http://pepsized.com/how-to-recreate-the-new-e-bay-site-scrolling-effect/?utm_source=CSS+Weekly&utm_campaign=CSS_Weekly_Issue_33&utm_medium=web" target="_blank">How to recreate the new e-bay site scrolling effect</a>

<a href="http://www.w3cplus.com/content/css3-box-sizing" target="_blank">CSS3 Box-sizing </a>

<a href="http://www.w3school.com.cn/css/pr_background-attachment.asp" target="_blank">CSS background-attachment 属性</a>

內容如有錯誤，歡迎指正
