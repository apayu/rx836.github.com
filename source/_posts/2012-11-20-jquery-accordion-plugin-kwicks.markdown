---
layout: post
title: "[jQ-Plugin] Accordion Menu(手風琴)-Kwicks"
date: 2012-11-20 11:52
comments: true
categories: jQuery jQ-Plugin
---

<img src="https://lh3.googleusercontent.com/-_J-W2xu9kk0/UKssWB_LsAI/AAAAAAAAB8I/l5FDpuCO27c/s415/t1.jpg" />

<img src="https://lh5.googleusercontent.com/-jKM2KBpI5eM/UKssWHgRekI/AAAAAAAAB8E/hG205WtoTDU/s415/t2.jpg" />

「jQuery accordion menu」，也有人稱呼為手風琴，從上面兩張圖可以看到原本是一個水平的menu，滑鼠移過去指定某個項目，週遭的menu會縮起來，指定的那個項目會展開，因為一開一合的效果很像手風琴，所以才稱呼為「accordion menu」

<!--more-->

但這篇不教怎麼自己打造accordion menu，因為自認為功力不夠不敢亂現，網路上也很多那種例如「30種精選jQuery accordion menu」主題的文章，資源非常豐富，但因為實在太多款了，每次要做都還要花時間一個一個去看，所以今天就特別介紹一款叫做 <a href="http://devsmash.com/projects/kwicks" target="_blank">「Kwicks」</a> 的jQuery plugin，也可以簡單達到前面所說的accordion menu效果，這邊就記錄在我的Blog裡面，方便我或網路上的朋友可以參考

最好的介紹就是直接看Demo最快，Kwicks可以做到 <a href="http://devsmash.com/projects/kwicks/examples/horizontal" target="_blank">Horizontal</a>、<a href="http://devsmash.com/projects/kwicks/examples/vertical" target="_blank">vertical</a>、<a href="http://devsmash.com/projects/kwicks/examples/easing" target="_blank">Custom Easing</a> 等效果

要用Kwicks需下載他的plugin還有jQuery

<a href="http://jquery.com/" target="_blank" />jQuery >= 1.7</a>

<a href="https://github.com/jmar777/kwicks/blob/v2.0.0/jquery.kwicks.js" target="_blank" />jquery.kwicks.js</a>

<a href="https://github.com/jmar777/kwicks/blob/v2.0.0/jquery.kwicks.css" target="_blank" />jquery.kwicks.css</a>

要注意的是，這版Kwicks是v2.0.0，需用到jQuery 1.7以上，另外如果要用到Custom Easing，還要另外下載jQuery Easing Plugin

<a href="http://gsgd.co.uk/sandbox/jquery/easing/" target="_blank" />jQuery Easing Plugin</a>	

接著就是HTML部分，很簡潔不複雜

	<ul class='kwicks kwicks-horizontal'>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
	</ul>
	
就是用一個&lt;ul&gt;元素包裹著&lt;li&gt;，&lt;li&gt;裡面放著就是項目裡面要擺的東西(例如圖片、文字)，&lt;ul&gt;部分必須要添加「kwicks」和「kwicks-horizontal」兩個class，「kwicks」是固定要添加的class，「kwicks-horizontal」是指水平的呈現方式，如果要垂直就用「kwicks-vertical」

jQuery的寫法部分，有分三種

	// instantiate kwicks
	$(element).kwicks(opts);

	// invoke a method
	$(element).kwicks('method-name' [, param]);

	// handle events
	$(element).on('event-name.kwicks', handler);

以下是參數設定

### size:(必填)

設定項目的長或寬，如果isVertical是true的話，這個設定就是高度，其它情況預設就是寬度，特別注意的是這個值會影響到整個accordion menu多高(或多寬)

### maxSize|minSize:(必填)

展開的最大寬度(或高度)，或是最小寬度(或高度)，你只能選擇填最大或最小，不能兩個都填

### spacing:(Default: 5)

每個項目之間的距離，預設是5px
    
### duration:(Default: 500)

    觸發後動畫執行的時間(毫秒)，預設是500毫秒
	
###isVertical:(Default: false)

	是否為垂直menu，預設是false
    
easing:(Default: none)

	如果有載入jQuery Easing Plugin，可以設定效果
    
behavior:(Default: none)

    初始化的動作
	
### Examples

HTML

	<ul class='kwicks kwicks-horizontal'>
		<li id='panel-1'><img src="pic.jpg" /></li>
		<li id='panel-2'><img src="pic.jpg" /></li>
		<li id='panel-3'><img src="pic.jpg" /></li>
		<li id='panel-4'><img src="pic.jpg" /></li>
	</ul>

用&lt;ul&gt;、&lt;li&gt;做一個menu，&lt;ul&gt;加上對應的class，&lt;li&gt;裡面放置圖片或文字
	
CSS
	
	.kwicks {
		width: 515px;
		height: 100px;
	}
	.kwicks > li {
		width: 100px;
		height: 100px;
		/* overridden by kwicks but good for when JavaScript is disabled */
		margin-left: 5px;
		float: left;
	}

	#panel-1 { background-color: #53b388; }
	#panel-2 { background-color: #5a69a9; }
	#panel-3 { background-color: #c26468; }
	#panel-4 { background-color: #bf7cc7; }
	
注意width和height會影響到顯示的結果
	
JS
	
	$(function() {
		$('.kwicks').kwicks({
			size: 100,
			maxSize : 250,
			spacing : 5,
			behavior: 'menu'
		});
	});
	
size要特別注意的是，越高(or寬)展開的空間就越大，看到的東西就會越多，如何拿捏可以實際在瀏覽器上跑跑看效果

Kwicks還有支援**Methods**和**events**，有興趣的可以直接參考文件(附參考資料)

當然，網路世界的選擇太多了，不一定非要用這個plugin，如果有更好的推薦也歡迎跟我說:)

參考資料:

<a href="http://devsmash.com/projects/kwicks" target="_blank">Kwicks for jQuery</a>

內容如有錯誤，歡迎指正
	
