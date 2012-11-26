---
layout: post
title: "[CSS] CSS3 box-shadow-用一個div畫出IPHONE 4"
date: 2012-11-26 10:21
comments: true
categories: CSS
---

<img src="https://lh3.googleusercontent.com/-gnXY1RrRaSU/ULLgp4EX-6I/AAAAAAAAB84/m3JLnkc5h_E/s125/a.jpg" />

CSS3有許多讓人驚艷的地方，其中之一就是「box-shadow」，在這之前為了做出陰影效果，可能需要一些Photoshop的幫助，但在CSS3卻可以用純CSS來達到這樣的結果，但如果你認為「box-shadow」只能拿來做陰影效果的話，那可就誤會大了，看完這篇文章，你或許會有不同的想法

<!--more-->

在此之前，我們先來介紹 **box-shadow** 一些基本的屬性和用法

**x-offset**: 水平位移植，必須要指定

**y-offset**: 垂直位移植，必須要指定

**blur**: 模糊效果，不能為負值，預設為0

**spread**: 擴散強度，可以為負值(縮小)，預設為0

**color**: 顏色，有些網站可能會寫預設值為黑色，**但一般建議還是要給予顏色，因為有些瀏覽器預設值並不一定為黑色(例如手機)**

**inset**: 這個值有些人是放在**最前面**，有些是放在**最後面**，兩者皆可，如果有給予這個值box就會在陰影裡面，反之則在外面

以下為box-shadow語法

	box-shadow: inset x-offset y-offset blur spread color
	
記得x-offset和y-offset為必要值，其它依照排列，如果只有blur可不填spread，但有spread一定要給blur值(可以為0px)

特別注意的是，**spread**這個屬性值，等等會來好好說明，先來看幾個簡單的範例

以下的範例HTML部分都只有這一行
	
	<div class="shadow"></div>

###X and Y Offsets

<pre class="_cssdeck_embed" data-pane="output,css" data-user="rx836" data-href="mo08pkqb" data-version="0"></pre><script async src="http://cssdeck.com/assets/js/embed.js"></script>

這邊建立了一個width和height都為100px的box，然後陰影依照這個box往右位移10px，往下位移10px，且顏色為黑色

###Inset

<pre class="_cssdeck_embed" data-pane="output,css" data-user="rx836" data-href="eesxhanx" data-version="0"></pre><script async src="http://cssdeck.com/assets/js/embed.js"></script>

如果有給予 **inset**，box就會在陰影裡面

###Blur

<pre class="_cssdeck_embed" data-pane="output,css" data-user="rx836" data-href="vic8fc7f" data-version="0"></pre><script async src="http://cssdeck.com/assets/js/embed.js"></script>

添加 **Blur** 值，會讓陰影有模糊效果

###Colors

<pre class="_cssdeck_embed" data-pane="output,css" data-user="rx836" data-href="zcpl4thp" data-version="0"></pre><script async src="http://cssdeck.com/assets/js/embed.js"></script>

也可以加些不一樣的顏色，這裡是給予rgba值

###spread

剛剛有特別要注意到 **spread** 這個值，原因就是他可以擴展陰影的範圍，可以放大可以縮小，但不能改變形狀，因為陰影的形狀是來自box(就跟人的影子一樣)，也就是box是圓形，陰影就是圓形，是方形就是方形

<pre class="_cssdeck_embed" data-pane="output,css,html" data-user="rx836" data-href="qnznlsof" data-version="0"></pre><script async src="http://cssdeck.com/assets/js/embed.js"></script>

如果spread為5px，那陰影就會擴展5px，如果為-5px，那陰影就會縮減5px，也就是說可以依照需求改變陰影的大小，這樣可以幹嘛呢？可以看看下面這個範例

<pre class="_cssdeck_embed" data-pane="output,css,html" data-user="rx836" data-href="qmbxujts" data-version="0"></pre><script async src="http://cssdeck.com/assets/js/embed.js"></script>

看到了嗎？我可以用**一個div就創造出這麼多個box**，也就是說我可以用一個元素來做出很多意想不到的效果，例如

我可以用一個div畫出一支IPHONE 4

<a href="http://cssdeck.com/labs/creating-single-element-iphone-using-css3" target="_blank"><img src="https://lh3.googleusercontent.com/-L9BuoRAjjfE/ULLjV_tNNGI/AAAAAAAAB9Y/SSAO9DOdBMU/s558/rr.jpg" /></a>

或用一個div畫出蒙娜麗莎的微笑

<a href="http://cssdeck.com/labs/mona-lisa-with-pure-css" target="_blank"><img src="https://lh5.googleusercontent.com/-gzi2x2_clBk/ULLjV4zuCnI/AAAAAAAAB9g/Oo9VmXXkF_E/s535/rr1.jpg" /></a>

甚至是利用這個原理，來當作畫Pixel圖案來使用

<a href="http://cssdeck.com/labs/create-a-pixel-character-using-css3-box-shadows" target="_blank"><img src="https://lh6.googleusercontent.com/-lnfW4QAeeao/ULLjV84Z0oI/AAAAAAAAB9c/1J0e5V0VjS0/s300/rr2.jpg" /></a>

所以好好運用box-shadow，他可以發揮許多意想不到的創意喔

參考資料:

<a href="http://codetheory.in/the-real-beauty-of-css3-box-shadows/" target="_blank">The Real Beauty of CSS3 Box Shadows</a>

<a href="http://www.w3schools.com/cssref/css3_pr_box-shadow.asp" target="_blank">CSS3 的box-shadow屬性</a>

內容如有錯誤，歡迎指正