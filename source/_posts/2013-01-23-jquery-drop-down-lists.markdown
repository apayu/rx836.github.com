---
layout: post
title: "[jQ-Plugin] 用jQuery客製化下拉選單"
date: 2013-01-23 17:16
comments: true
categories: jQ-Plugin
---

下拉式選單(DropDownList)在表單填寫裡面，是很常用到的網頁元素，但原生的下拉式選單看久了，難免會覺得太過單調，有時為了配合整體網站的設計，會有客製化的需求，而這篇文章主要是介紹如何用 jQuery plugin 客製化下拉選單

<!--more-->

另外對客製化 CheckBox 有興趣的朋友，也可以參考 <a href="http://blog.rx836.tw/blog/css3-checkboxes-radiobuttons/" target="_blank">[CSS] 拋棄原生checkbox用CSS3自己簡單動手做</a> 這篇文章

##Start

這裡我主要用的是 jquery.dropdown.js 這支plugin，首先要先下載js和css回來

<a href="http://tympanus.net/Development/SimpleDropDownEffects/SimpleDropDownEffects.zip?84cd58" target="_blank">DOWNLOAD SOURCE</a>

在js的資料夾裡面有兩個檔案，分別是

jquery.dropdown.js

modernizr.custom.63321.js

連同 jQuery 載入到網頁裡面

	<script src="js/modernizr.custom.63321.js"></script>
    <script type="text/javascript" src="http://code.jquery.com/jquery-1.8.2.js"></script>
	<script type="text/javascript" src="js/jquery.dropdown.js"></script>
	
會用到 modernizr 是因為在 jquery.dropdown.js 這支檔案裡面有用到判斷是否支援transition，稍後會提到

接著是html部份

	<select id="cd-dropdown" class="cd-select">
		<option value="-1" selected>請選擇一種動物</option>
		<option value="1" class="icon-monkey">猴子</option>
		<option value="2" class="icon-bear">熊</option>
		<option value="3" class="icon-squirrel">松鼠</option>
		<option value="4" class="icon-elephant">大象</option>
	</select>

js部份，一行程式碼很簡單明瞭

	$( function() {
				
		$( '#cd-dropdown' ).dropdown();

	});
	
css部份

利用 plugin 做客製化下拉選單，關鍵就在於將原生的&lt;select&gt;用jQuery替換掉，仔細看替換掉後的html結構，會發現其實長的像這樣

	<div class="cd-dropdown">
		<span>請選擇一種動物</span>
		<input type="hidden" name="cd-dropdown">
		<ul>
			<li data-value="1"><span class="icon-monkey">猴子</span></li>
			<li data-value="2"><span class="icon-bear">熊</span></li>
			<li data-value="3"><span class="icon-squirrel">松鼠</span></li>
			<li data-value="4"><span class="icon-elephant">大象</span></li>
		</ul>
	</div>
	
利用新的html結構就可以藉由CSS來自行裝飾，就像下面結果圖一樣，這邊我是直接用範例所附的css檔

<img src="https://lh5.googleusercontent.com/-evzDeROGJXM/UP_5cKXoSNI/AAAAAAAACOc/GgnPHX_BsjQ/s328/2013-01-23_220729.jpg" />

<img src="https://lh5.googleusercontent.com/-jM7YmJVygBs/UP_5cFenQ8I/AAAAAAAACOY/PzAILoleuwo/s345/2013-01-23_220659.jpg" />

###modernizr

前面有提到使用 modernizr 的關係是因為有些瀏覽器不支援transition，但自己要寫那些判斷程式又稍嫌麻煩，而 modernizr 正是解決這方面需求的js函式庫，藉由函式庫我們可以透過 class 的名稱來做判斷，例如 firefox 有支援 transition 的話，在html上會看到 class 名稱為 csstransitions

<img src="https://lh4.googleusercontent.com/-7d8Z_8f3zqI/UP_5cDplfCI/AAAAAAAACOU/FuEhK0BRsd4/s452/2013-01-23_221311.jpg" />

IE9沒支援 class 名稱就是 no-csstransitions

<img src="https://lh3.googleusercontent.com/-G-9zngyNiH4/UP_5dLraQhI/AAAAAAAACOk/foYV278aKs0/s401/2013-01-23_221500.jpg" />

所以剛提到主程式裡面，判斷的程式碼就像這樣

	if( Modernizr.csstransitions ) {
		setTimeout( function() { self.opts.css( 'transition', 'all ' + self.options.speed + 'ms ' + self.options.easing ); }, 25 );
	}

###更不一樣的下拉選單

這款 plugin 還有提供一些參數做變化，例如給予的參數值像下面這樣

	$( '#cd-dropdown' ).dropdown( {
		gutter : 5,
		delay : 40,
		rotated : 'left'
	} );

其中　rotated　就是旋轉的方向，再搭配css就可以做出更有特色的下拉選單

<img src="https://lh6.googleusercontent.com/-McvNbs1qkQs/UP_5daenx8I/AAAAAAAACOo/pfBHIHJWFyQ/s471/2013-01-23_223858.jpg" />

##總結

在使用上會發現一個問題就是，每當網頁載入時，**因為要透過js來做替換html結構**，所以會先看到原生的下拉選單元素，然後瞬間才會換成客製化元素，難免會覺得不夠細膩，但假如了解他運作的方式，直接自己製作html而不用經過 jQuery plugin 更換，會是更好的方法

##參考資料:

<a href="http://tympanus.net/codrops/2012/11/29/simple-effects-for-drop-down-lists/" target="_blank">SIMPLE EFFECTS FOR DROP-DOWN LISTS</a>

<a href="http://modernizr.com/" target="_blank">modernizr</a>

內容如有錯誤，歡迎指正



