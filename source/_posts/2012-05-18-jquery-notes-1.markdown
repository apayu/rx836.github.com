---
layout: post
title: "[Jquery]jquery使用筆記(一)"
date: 2012-05-18 12:17
comments: true
categories: 
---
從08年那時候剛接觸到jquery，到現在每天都在使用他，總覺得好像不為自己寫一下筆記使用心得，也有點不踏實，重點是，我好像也沒什麼"材料"可以貢獻在廣大的技術社群裡面，只能從我會一點皮毛的地方開始寫起真正的程式筆記心得，希望能從這開始發芽....，最後長成大樹(無尾熊?疑?)
<!--more-->

近一兩年所呈現的網頁，網站越來越重視所謂互動效果，隨著瀏覽器的執行速度越來越快，就有越來越多的特效與動畫，出現在網際網路世界裡，廢話不多，直接擺上例子

<a href="http://jquery.malsup.com/cycle/" target="_blank">jQuery Cycle Plugin</a>

<a href="http://jquery.malsup.com/block/#page" target="_blank">jQuery BlockUI Plugin (v2)</a>

在以前可能會覺得非常的酷炫，可是現在似乎沒有加幾個特效好像就不叫一個網頁(?)這些用原生的javascript都可以自己刻出來，但在現在凡事求快的情況下，一個案子可能沒那麼多時間慢慢寫這些東西，更何況還有令人聞之喪膽的跨瀏覽器問題

所以在這個情況下，用javascript所寫的一個library就這麼誕生了，不僅解決了跨瀏覽器的問題，更重要的是，他運用了很多HTML與CSS的原理，使的設計人員可以在會一點點的JS情況下，完成這些效果

而對於開發人員來說，強大的plugin社群，更是縮減了不少開發時間，就如同剛剛那兩個範例連結，當然，還有其他更多更好的優點如下

####強大的選擇器、輕鬆找到你要的元素 例:尋找class名稱為myName，底下所有的a標籤####

	$('.myName').find(a);
	

####改變頁面的呈現樣式 例:替所有div增加一個名為myStyle的class####

	$(div).addClass('myStyle');
	
####改變網頁內容 例:在body底下額外增加html標籤####

	$(body).append('<div>my html</div>');
	
	
####與使用者做互動 例:點擊button後alert出一個視窗####

	$(button).click(function(){
		alert('good!');
	});

####簡單的動畫增加良好的使用者經驗 例:簡單在div做fading效果####

	$(div).fadeIn();
	
####支援AJAX效果 例:載入article.html####

	$('#a').load('article.html');
	
####利用迭代的特性簡化javascript 例:分別alert出a,b,c####

	var a1=["a","b","c"];
	$.each(a1,function(){
		alert(this);
	});

可能有些人會覺得，現在市面上的library 這麼多，為什麼一定要選Jquery?當然，你也可以選擇別的library沒錯，那這篇筆記我們就到這邊吧...ㄟ!當然不是呀，為什麼Jquery能有這麼廣泛的使用者，一定是有他的原因的是吧?

####利用css的知識原理架構####

Jquery繼承了CSS強大的選擇器，這讓許多網頁設計者，可以利用自有本身的CSS知識來撰寫Jquery，而不用擔心因為程式的門檻關係，而降低使用特效的學習曲線

####支援擴充####

你可以修改別人的plugin，也可以自己撰寫一個plugin，甚至將好幾個plugin合在一起來個大雜燴也可以，減少重造輪子

####解決跨瀏覽器的問題####

我想這不用說了，一切都是IE造就了Jquery的蓬勃發展(誤)

####超方便的隱式迭代(implicit iteration)####

如果要將所有的div做隱藏，在以前我們可能要先將div都找出來，然後再用for迴圈一個一個隱藏，但Jquery說:不用! 只要這樣寫就好了!

	$(div).hide();
	
這裡的div其實是所有的div集合，利用這種特性，就可以減少很多程式碼的撰寫

####鍊式(Chaining)語法的魔力####

Jquery可以跟串香腸一樣，把許多動作串成一行程式，增加程式的效率，也不用再定義一堆變數

	$(div).show().addClass('a');

####富爸爸和全世界強大的社群力量####

這當然是最重要的一部份啦，除了微軟支援他以外，全世界有這麼多人使用，還怕找不到教學與範例可以複製貼上嗎?(誤)

好了，講了那麼概念，還是要動手開始實做一次

###首先下載Jquery###

你可以到<a href="http://docs.jquery.com/Downloading_jQuery" target="_bland">Jquery Download</a>下載Jquery回來，或是使用Google CDN或Microsoft CDN，他有分壓縮過後的版本和沒壓縮過後的版本，一般來說開發階段可以使用開發版本

###引入Jquery文件###

將jquery引入到你的web頁面，一般是放在head裡面，底下是引入Google  API CDN

	<head>
		<script  src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
	</head>

接著在body裡面加上簡單的HTML

	<div class="btnClass">點我</div>
		<div class="showClass">
    		<p>one</p>
    		<p>two</p>
    		<p>there</p>
	</div>
	
然後在script標籤裡面加上這段語法

	$(document).ready(function() {
    		$('.btnClass').click(function(){
        		$('.showClass>p').eq(0).hide();
    		});
	});
	
這裡我們做簡單的程式解說，目的是想讓讀者了解如何使用Jquery，詳細的部分都會在未來的筆記多做介紹，首先是Jquery的選擇器$()，你可以在選擇器裡面利用CSS語法字串，來選取你想要的元素，例如選取class名稱為a的元素
	
	$('.a')
	
或是選取ID名為b底下的a標籤

	$('#b a')
	
這裡我們所選擇的是class名為btnClass的元素，接著$()會將選取的元素$('.btnClass')封裝成一個Jquery物件，並且回傳，這時候就利用剛剛所講的**鍊式Chaining**，給予他一個click事件，而我們這邊可以榜定一個函在這個click事件裡面，當點擊btnClass時可以執行這個**函式(function)**，我們在函式裡面加了$('.showClass>p').eq(0).hide();這行程式碼
，這裡會看到一個比較特別的方法**eq()**，我們前面曾經提過，$()裡面是包含所選取的元素集合，所以可以利用eq()方法來選取我們想要的元素，eq()裡面指定一個index，這裡我們想指定第一個，所以是eq(0)，接著在Chaining一個hide()的方法，我們就完成基本的程式語法結構


#等等!#

$(document).ready()是什麼東西?!


說到**$(document).ready()**這個語法常會拿**window.onload**這個語法一起比較，簡單的來說window.onload是JS的原生事件，觸發的時機是整個網頁都載下來(包含圖片)時，而$(document).ready是在DOM元素下載下來後就先觸發，他是使用DOM標準的DOMContentLoaded事件，意思就是不需要等圖片載完，好處就是觸發時間比較早，而DOMContentLoaded其實是firefox的DOM事件，IE其實是要用其他特殊處理才能達到一樣效果，但! Jquery的好處就在這裡，已經幫你把跨流覽器的問題處理好了!!

介紹完Jquery程式碼部分接著就可以開啟瀏覽器執行，當你點擊**點我**時，**one**就會消失不見

神奇吧!!只需要這幾行程式碼!

<a href="http://jsfiddle.net/RNCVB/1/" target="_blank">線上範例</a>






