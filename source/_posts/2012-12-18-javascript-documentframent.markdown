---
layout: post
title: "[JavaScript] DocumentFragments-JS加快效能的好物"
date: 2012-12-18 14:38
comments: true
categories: JavaScript
---

JavaScript裡面有個物件叫DocumentFragments，它不算是新的觀念或新的技術，但我則是最近才認識到他，會想筆記這篇是因為他在操作DOM這方面的效能頗為出色，不過真的實驗下來好像只有某幾個瀏覽器或是版本才有明顯的效果，User的環境不同好像也會有些許的差異，下面就來看看用法和實際測試的結果

<!--more-->

##實驗開始

假設一個情況，我們有時候可能要大量的動態增加元素，例如很多很多的&lt;div&gt;，我們會這樣寫

	function CreateNodes(){
		for( var i=0; i<10000; i++ ) {
			var item = document.createElement('div');
			$(item).text('div-'+i);
			$(item).css({
				background: 'blue',
				padding: 5,
				margin: 5,
				float: 'left'
			});
			$('body').append(item);
		}
	}
	
這裡我們利用for迴圈增加了10000個div，不過這裡有個缺點，就是每一次新增一個div，都會對browser做一次『更新頁面』這個動作，所以如果新增10000個&lt;div&gt;，就會有一萬次的更新

再來我們看看DocumentFragment的寫法

	function CreateFragments(){
		var fragment = document.createDocumentFragment();
		for( var i=0; i<10000; i++ ) {
			var item = document.createElement('div');
			$(item).text('div-'+i);
			$(item).css({
				background: 'blue',
				padding: 5,
				margin: 5,
				float: 'left'
			});
			fragment.appendChild(item);
		}
		$('body').append(fragment);
	}
	
關鍵點在於多了一個 **document.createDocumentFragment()** 這個物件，這個物件是一個虛擬的DOM節點，它可以增加元素在這個虛擬節點上面，就跟正常DOM差不多，但因為他是虛擬的，所以browser並不會做更新這個動作，而最後再把DocumentFragment裡面的元素一次加到body裡面，這有點像是buffer(緩衝區)的效果

最後我用了手邊的瀏覽器測了一下結果

**Firefox 17.0.1:**

用DocumentFragment反而慢了0.6~0.8秒左右

**Google Chrome 23.0.1271.97:**

沒有明顯的差別

**IE9:**

用了DocumentFragment大概10秒左右就可以載完畫面，沒用大概要花上20幾秒...

##結論

這裡有個 <a href="http://jsperf.com/out-of-dom-vs-documentfragment/3" target="_blank">網站</a> 裡面有各個瀏覽器版本的測試報告，有興趣的可以參考看看，整體看下來DocumentFragment的確可以有效改善操作DOM的效能，我的想法是，其實現在的瀏覽器速度越來越快，有時候真的很難感受的到那幾毫秒的差距，但如果要顧慮到支援舊有的瀏覽器，那效能部分可能就要注意一下，不過適時的提醒用戶，想要有順暢的體驗，還是擺上Chrome或Firefox的下載連結其實也是不錯的


###參考資料:

<a href="http://davidwalsh.name/documentfragment" target="_blank">JavaScript DocumentFragment</a>

<a href="http://jsperf.com/out-of-dom-vs-documentfragment/3" target="_blank">out of dom vs documentfragment</a>

<a href="http://www.hujuntao.com/archives/using-documentfragment-speed-up-dom-rendering.html" target="_blank">利用DocumentFragment加快DOM渲染速度</a>

<a href="http://fstoke.me/blog/?p=2487" target="_blank">使用DocumentFragment來加快DOM操作速度</a>

內容如有錯誤，歡迎指正
