---
layout: post
title: "[jQuery] $.data原理"
date: 2012-08-30 14:10
comments: true
categories: jQuery
---

今天在看別人寫的jQuery Plugin，發現 **this[expando]** 這個寫法，好奇心驅使下，決定一探究竟

<!--more-->

因為不了解**expando**是甚麼，所以特地去找了一下Google，發現在jQuery裡面有這一段程式碼
	
	expando: "jQuery" + ( jQuery.fn.jquery + Math.random() ).replace( /\D/g, "" );
	
原來這是在使用$.data時可以做為匹配的id，產生的邏輯就是版本代號+一組亂數，並把非數字的字元用replace替代掉，expando會在每次載入jQuery時直接生成，所以用console.log()看如下面所示

	console.log($.expando);
	//jQuery18004247503886623739

那$.data又是甚麼呢？在jQuery的文件裡面是這樣寫

	Description: Store arbitrary data associated with the matched elements.
	
意思就是以前我們都喜歡將數據存在HTMLElement屬性上，例如下面所示

	<div data="some data">my div</div>
	<script>
		div.getAttribute('data'); //some data
	</script>
	
但如果用這種方式添加數據，往往數據會直接曝露在原始碼當中，從安全性的角度來思考並不太好，另一方面，在DOM的元素中添加這麼多的屬性，其實對瀏覽器來說是沒有意義

所以jQuery很棒的提供了這方面的解決方式給我們，利用$.cache來緩存我們想要保存的數據，在說明原理之前，我們先來看幾個參數的意義，在jQuery原始碼底下看到以下這些程式碼

	
	jQuery.extend({
	
		cache: {},
		
		...

		// Please use with caution
		uuid: 0,

		// Unique for each copy of jQuery on the page
		// Non-digits removed to match rinlinejQuery
		expando: "jQuery" + ( jQuery.fn.jquery + Math.random() ).replace( /\D/g, "" ),

		// The following elements throw uncatchable exceptions if you
		// attempt to add expando properties to them.
		noData: {
			"embed": true,
			// Ban all objects except for Flash (which handle expandos)
			"object": "clsid:D27CDB6E-AE6D-11cf-96B8-444553540000",
			"applet": true
		},

		hasData: function( elem ) {
			elem = elem.nodeType ? jQuery.cache[ elem[jQuery.expando] ] : elem[ jQuery.expando ];
			return !!elem && !isEmptyDataObject( elem );
		},
		
		...
		
	});
	
**jQuery.cache**:空物件，用來做緩存

**jQuery.uuid**:一個seed，會遞增，用來標示每個cache

**jQuery.expando**:一組字串，如前面所說，由Math.random生成，同時也是DOM的屬性名稱，裡面會對映到jQuery.uuid

**jQuery.noData**:檢查元素是否能使用$.data，預設是embed、object、applet不能使用

**jQuery.hasData**:判斷元素是否已經擁有data

接下來是範例講解

	<div>test</div>
	<script>
		console.log($.expando);
		//jQuery180010448733290775436 
		//載入jQuery就會生成一組字串
		
		var div = document.getElementsByTagName('div')[0];
		
		console.log($.hasData(div));
		//false
		//因為div還沒使用$.data，所以為false
		
		$.data(div,'divName','name1');
		
		console.log($.hasData(div));		
		//true
		//div已經有包含data，所以為true
		
		console.log($.uuid);
		//1
		//第一個cache，此時seed遞增為1
		
		var div2 = document.getElementsByTagName('div')[1];		
		
		$.data(div2,'divName','name2');
		
		console.log($.uuid);
		//2
		//第二個chche，此時seed遞增為2
		
		var myObj = {};
		
		$.data(myObj, 'objName','name3');		
		
		console.log($.data(myObj, 'objName'));
		//name3
		//不只是HTMLElement可以使用$.data，物件也可以使用$.data
		
		console.log(myObj);		
		//myObj ={
		//	jQuery180010448733290775436:{
		//		objName:name3
		//	}
		//}
		//不過物件並沒有將data緩存到$.cache裡面，而是直接在物件裡面新增一個屬性
		//屬性名稱為$.expando，值為剛剛設定的緩存值
		
		console.log(div[$.expando]);
		//1
		//再回頭看看元素div會發現裡面已經添加屬性，屬性名稱就叫$.expando也就是最前面那串字串
		//而屬性值就是1		
		
		console.log($.cache);
		//1:{divName:'name1'}
		//2:{divName:'name2'}		
		//只有HTMLElement元素才會將值緩存到$.cache裡面，而且會發現屬性值為1可以匹配到$.cache裡面的屬性
	</script>
	

用圖表示關係如下

<img src="https://lh5.googleusercontent.com/-t5d07KuRuJk/UD8Yz5NlG6I/AAAAAAAABYg/cd1cmEgctH8/s748/1.jpg" width="700px" />

巧妙的使用$.data，就可以不必替DOM元素新增一堆屬性了

參考資料:

<a href="http://api.jquery.com/data/" target="_blank">jQuery $.data</a>

<a href="http://www.jb51.net/article/27433.htm" target="_blank">http://www.jb51.net/article/27433.htm</a>

<a href="http://hpf1908.appspot.com/2010/10/7/cache-jquery-javascript.html" target="_blank">http://hpf1908.appspot.com/2010/10/7/cache-jquery-javascript.html</a>

如有錯誤，歡迎指正