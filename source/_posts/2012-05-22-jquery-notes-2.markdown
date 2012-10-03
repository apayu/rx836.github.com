---
layout: post
title: "[jQuery]jquery使用筆記(二)-選擇器*開罐器"
date: 2012-05-22 00:20
comments: true
categories: jQuery
---

其實選擇器就像開罐器一樣，會用這個工具的人，自然吃的到甜頭，但不會用這個工具的人，不管罐頭裡面的麵筋土豆有多美味，吃不到就是吃不到，就如同jquery再怎麼強大，也只能看著螢幕，而不知該如何下手，不過雖然選擇器不難，也容易上手，但老實說，我用了一年多下來，還是覺得自己只有用皮毛而已，所以希望藉著這一系列的筆記，讓自己能更長進一些
<!--more-->

##DOM怎麼吃##

<a href="http://www.ideastar.me/2011/11/htmljs-dom.html" target="_blank">DOM</a>可以說是JavaScript與網頁之間的聯繫管道，他提供了一個模型，讓JavaScript能藉由此模型來改變或操作整個網頁，

	<div class="one">
		<p>two_1</p>
		<p>two_2</p>
		<p>two_2</p>
	</div>

我這邊就簡單介紹一下DOM模型，有個元素class名為one的是父元素，底下有三個兒子元素&#60;p&#62;，每個元素都視為一個節點，也可以看成一個樹狀圖，因為我認為有些東西是Google會講得比我好，所以還想知道更多糾結的父子關係...，可以<a href="http://www.ideastar.me/2011/11/htmljs-dom.html" target="_blank">去這</a>，那邊有很好的說明，這邊就不多加解釋，而當Jquery利用選擇器抓取到DOM元素以後，就會將他包裝成一個Jquery object，並且回傳

##$('#MyDiv')&#60;-- 他是一個物件##

這裡有個觀念十分重要，因為許多初學者，甚至是一些從Jquery開始學起Javascript的開發者(包括我)，常常會把以下兩個程式碼搞混在一起

	//原生JavaScript取id為a的div
	var result1 = document.getElementById('a');
	console.log(result1);
	
	//用jquery取id為a的div
	var result2=$('#a');
	console.log(result2);

如果你執行這段程式碼出來，妳會發現console出來的結果，用JavaScript取出來的結果是DOM，可是一樣的div用Jquery取出來的卻是個包裝過後的物件，換句話說，你不能直接對包裝過後的Jquery物件增加**DOM的事件**，而是要用**Jquery提供的事件**，有人會說，那意思是不是說以後只能河水不犯井水，往後互不干涉，從此分道揚鑣呢? 到也不是

	var b=$('#a')[0];
	
只要跟上述程式碼一樣就可以取得DOM的元素了

##$()工廠##

不管是如何選擇，我們都會用相同的函式**$()**，就如之前所講的，他能接受CSS選擇器的語法做為參數，而最主要的三個參數分別為tag name、ID與class，當然，這三個參數可以再與其他CSS語法做結合

	//tag name
	$('div')
	
	//ID
	$('#myId')
	
	//class
	$('.myClass')
	
而上述函式都會如同第一章所介紹的，都有隱式迭代的特色，而為了做到跨覽器的支援，Jquery的選擇器包含了CSS1-3，所以不用擔心一些比較特別的瀏覽器(對就是IE6)不能執行，除非瀏覽器沒有開啟JavaScript

接著接下來我簡單介紹幾個用法

<a target="_blank" href="http://jsfiddle.net/XZnQ7/">http://jsfiddle.net/XZnQ7/</a>

	//將不含color1 class的p增加一個color2 class
	$('p:not(.color1)').addClass('color2');
	
<a target="_blank" href="http://jsfiddle.net/bpJct/3/">http://jsfiddle.net/bpJct/3/</a>

	//這裡是用正規表示法
	$('a[href^="mailto:"]').addClass('font1');
	$('a[href^="http"]').addClass('font2');
	$('a[href$=".pdf"]').addClass('font3');

當然還提供了一些客製化(custom)的選擇器，但一般來說原生(native)的方式會來的效能比較快，如果有注重這塊的朋友，可能要盡量避免使用客製化的選擇器例如以下範例

<a target="_blank" href="http://jsfiddle.net/MF8mu/">http://jsfiddle.net/MF8mu/</a>

	//替index為1的tr加上class
	$('tr:eq(1)').addClass('color1');

	//替index為1的tr加上class
	$('tr:nth-child(1)').addClass('color2'); 
	
這裡很特別的是，**為什麼都是替index為1的tr加上class，卻是不同的結果呢?**，因為:eq()算是一個JavaScript陣列，index是0起始，所以才會選到第二個，而nth-child()是CSS選擇器的一種，所以index是以1起始，選到的就是第一個，以下的範例意思相同

<a target="_blank" href="http://jsfiddle.net/3PrJt/">http://jsfiddle.net/3PrJt/</a>

	//選擇偶數的tr增加class
	$('tr:even').addClass('color1');
	
	//選擇偶數的tr增加class
	$('tr:nth-child(even)').addClass('color2');
	
就如同剛剛所講的，index起始不同(JavaScript起始為0，CSS為1)，所以雖然都是取偶數，但卻是不同列

再來就一些FORM常用的選擇器 <a target="_blank" href="http://jsfiddle.net/qcXSy/3/">http://jsfiddle.net/qcXSy/3/</a>

	$(':button').click(function(){
   		 alert('a');
	});
	
這就代表說綁定所有的bitton一個click事件，其他還有像:input、:button、:enabled、:disabled都可以跟其他選擇器一起組合成新的選擇器

##更加強大的.filter()##

當有時候一般的選擇器已經不能不能滿足我們複雜的DOM時，例如要抓div的爸爸的哥哥的兒子的妹婿的二姑的大舅時...，這時候還可以用一個方法filter，這個方法特別的地方在於他可以帶function進去 <a target="_blank" href="http://jsfiddle.net/wGz3k/">http://jsfiddle.net/wGz3k/</a>

可以看到function裡面限制return index == 1才可以增加CSS，這個好處就在於可以在裡面做很多複雜的邏輯運算

當然Jquery還有太多太多選擇器可以使用，像還有.next()、.parent()、.children()一般常用的這幾個，其實就很夠用了我認為，再多的選擇器有時候好像只是展示不同的寫法，但其實只要能抓取到你想要的元素，解決問題

你甚至想要這樣寫$('div').children().children().children().children().children()也不會有人說不行..

更多的選擇器可以到Jquery的官方網站<a target="_blank" href="http://api.jquery.com/category/selectors/">看文件</a>

以上如有錯誤或疑問，歡迎一起討論喔!
