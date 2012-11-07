---
layout: post
title: "[CSS] Data URI使用心得筆記"
date: 2012-11-07 16:02
comments: true
categories: CSS
---

Data URI不算新的技術，但他卻是一個可以節省頻寬，增進網頁載入效率的技巧，今天就來實際記錄一下使用的方式，順便比較一下用src指向URL的差別

<!--more-->

Data URI是直接在網頁崁入一段Base64編碼，目前IE8+,Firefox, Safari, Opera, Chrome都能正確顯示圖檔和css設定，以下是Base64編碼崁入在網頁的樣子

	<img src="data:image/png;base64,<base64 data goes here>" />
	
HTML碼中＜base64 data goes here＞就是擺放那一長串的文字編碼，現在就來實際操作一下如何使用

首先你必須要準備一張圖檔，如果不想找可以直接到<a href="http://subtlepatterns.com/" target="_blank">Subtle Patterns</a>下載

接著到<a href="http://www.websemantics.co.uk/online_tools/image_to_data_uri_convertor/" target="_blank">websemantics</a>，點選BROWSE選取要轉換成Base64編碼的圖片，按下CONVERT IMAGE

<img src="https://lh4.googleusercontent.com/-PmeBE4o7p7s/UJooOcgjcaI/AAAAAAAAB3o/qgNMNlvaSPA/s476/a.jpg" />

之後將網頁拉到最下方，會看到轉換出來的Base64編碼和CSS

<img src="https://lh6.googleusercontent.com/-UTJUZpoyHE4/UJooOR2uuQI/AAAAAAAAB3Y/jqioWsQHsw0/s651/b.jpg" />

接著直接將css複製到網頁上，並且增加另外一段css用src做比較

		div.logo-data  {
			width: 198px;
			height: 200px;
			background-repeat: no-repeat;
			background-image: url(data:image/png;base64,<base64 data goes here>);
		}	
		div.logo-img{
			width: 198px;
			height: 200px;
			background-repeat: no-repeat;
			background-image: url(nasty_fabric.png);			
		}

注意，＜base64 data goes here＞是要放Base64編碼，但因為實在太長了(這也是等下會提到的缺點之一)，所以我這邊用＜base64 data goes here＞代替

再來是HTML部分，我們先看用src直接指向URL的結果

	<div class="logo-img">
	</div>
	
打開Firebug，看看讀取這個網頁會載入些什麼

<img src="https://lh4.googleusercontent.com/-0vnZZFDEAb4/UJooOTvo1eI/AAAAAAAAB3c/k8REjQueAvI/s891/c.jpg" />

會看到載入了一個網頁和一個png圖檔，共70kB

接著用Data URI來看看

	<div class="logo-data">
	</div>
	
<img src="https://lh6.googleusercontent.com/-4uQB0YLPq7U/UJooPPLWN0I/AAAAAAAAB3k/74hpcikj_O0/s894/d.jpg" />

一樣的圖片呈現效果，這裡只載入一個網頁，圖片呢？圖片就如剛剛所說的，用base64編碼方式崁入在網頁裡面，所以網頁稍微大了一點點(因為那一長串的字串關係)，但卻可以減少一個HTTP Request

所以使用Data URI的好處就是不用下載圖檔，也不用占用到HTTP Request

但缺點就是除了一開始提到的IE8以上才支援以外，還有因為是崁入到網頁當中，所以如果是動態網頁內容會變化的話，就無法享受到快取的好處，而且整個HTML和css會看起來比較凌亂(一堆編碼)，再加上工作流程上也必須先將圖片處理過後，才能使用，會增加製作的時間

### 總結:

假如你放棄了IE8以下的瀏覽器，或許可以在一些背景圖和一些小icon做一些Data URI的處理，畢竟減少一些頻寬和HTTP Request也對$$也是不無小補:)

參考資料:

<a href="http://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/the-what-why-and-how-of-data-uris-in-web-design/" target="_blank">The What, Why and How of Data URIs in Web Design</a>

<a href="http://blog.darkthread.net/post-2010-11-05-data-uri.aspx" target="_blank">淺嚐Data URI</a>

內容如有錯誤，歡迎指正