---
layout: post
title: "[jQ-Plugin] 做出Pinterest效果的介面 用jQuery Masonry + Infinite Scroll"
date: 2012-06-19 00:27
comments: true
categories: jQuery jQ-Plugin
---

相信已經有很多人已經看過<a href="http://pinterest.com/" target="_blank">pinterest</a>這個網站的介面效果，是利用一個稱為<a href="http://www.21andy.com/blog/20120527/2041.html" target="_blank">Waterfall</a>，中文叫做瀑布流布局的效果，原理是算出周圍元素的寬和高，去排列畫面的布局，利用絕對定位的方式來達到隨著螢幕大小來變動整個版面

<!--more-->

再加上無限滾輪( Infinite Scroll)的搭配，就可以做出類似Pinterest效果，所以上網去搜尋了一下，找到了<a href="http://masonry.desandro.com/index.html" target="_blank">jQuery Masonry</a>這個Waterfall的Plugin，在jQuery Masonry的官方文件裡面寫可以跟<a href="http://www.infinite-scroll.com/" target="_blank">Infinite scroll</a>這個Plugin一起搭配無限滾輪這個效果，但我找不到Infinite scroll使用向Server端取得元素的方法，例如.NET常用的泛型處理常式，所以我另外找了其他的Infinite Scroll來使用

但其實可以按照個人所需來選擇，這裡有介紹<a href="http://designbeep.com/2011/08/12/12-jquery-infinite-scrollingscroll-read-plugins-for-content-navigation/" target="_blank">12種jQuery Infinite Scrolling</a>，而我這邊是選擇<a href="http://andersonferminiano.com/jqueryscrollpagination/" target="_blank">jQuery ScrollPagination</a>，因為對我來說使用起來很簡單，但缺點就是要稍微修改一下Plugin，對於IE8來說

首先就是先隨意建立一個HTML，但有個比較要注意的地方就是所有的div或是其他元素包含在_container裡面的，都要盡量去宣告width，不然有時候會有不正常的情況發生

	<div id="_container" style="height:800px;">	        
	        <div class="item"><div><img src="images/pic1.jpg" /></div><div>我要講的話我要講的話我</div> </div>
	        <div class="item"><div><img src="images/pic2.jpg" /></div><div>我要講的話我要講的話我要講的話我要講</div> </div>
	        <div class="item"><div><img src="images/pic4.jpg" /></div><div>我要講的話我要講的話我</div> </div>
	        <div class="item"><div><img src="images/pic5.jpg" /></div><div>我要講的話我要講的話我要講的話我要講的話我要</div> </div>
	        <div class="item"><div><img src="images/pic6.jpg" /></div><div>我要講的話</div> </div>       	
	</div>   

再來是js的部分，引用Jquery+jQuery Masonry+jQuery ScrollPagination

	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js" type="text/javascript"></script>
	<script type="text/javascript" src="scripts/jquery.masonry.min.js"></script>
	<script type="text/javascript" src="scripts/scrollpagination.js"></script>   
	
接著是要撰寫的部分，首先是Jquery Masonry部分，也就是Waterfall

	$('#_container').imagesLoaded(function () {
	        $('#_container').masonry({
	            // options
	            itemSelector: '.item',
	            columnWidth: 240,
	            singleMode: true,
	            animate:true
	        });
	});
	
**imagesLoaded()**:這個方法主要是因為一般來說我們用jquery用$(function(){ .. });這個方法來實做，image並不會載完，而是在DOM載完以後就會立刻執行，可是這樣並沒有辦法得知圖片大小，所以必須用imagesLoaded()來防止計算寬度和高度錯誤

**itemSelector**:要套用效果的元素

**columnWidth**:欄位寬度

**singleMode**:因為等會在jQuery ScrollPagination裡面也會再用一次Jquery Masonry(讀取新的元素進來要套用效果)，所以這邊設定true，後面的Jquery Masonry就可以直接使用前面的設定

**animate**:打開效果

接著是jQuery ScrollPagination的撰寫部分

	$('#_container').scrollPagination({
	        'contentPage': 'GetDynamicGrid.ashx', // the page where you are searching for results
	        'contentData': {  }, // you can pass the children().size() to know where is the pagination
	        'scrollTarget': $(window), // who gonna scroll? in this example, the full window
	        'heightOffset': 10, // how many pixels before reaching end of the page would loading start? positives numbers only please
	        'beforeLoad': function () { // before load, some function, maybe display a preloader div
	            
	        },
	        'afterLoad': function (elementsLoaded) { // after loading, some function to animate results and hide a preloader div
	
	            var $newElems = $(elementsLoaded).css({ opacity: 0 });
	            $newElems.imagesLoaded(function () {
	                // show elems now they're ready
	                $newElems.animate({ opacity: 1 });
	                $('#_container').masonry('appended', $newElems, true);
	            });
	        }
	    });
	    
這裡就不細翻每個option的解釋，大概的原理就是當算出scroll到底部以後，就會觸發ajax，接著afterLoad()會callback一個參數，裡面就是server端回傳的新元素，再用Jquery Masonry將Waterfall效果套用在新元素上面

##IE8的空白間格問題...##

但我在實做過程中，就如同之前所講的，IE8會有些許的問題，會發現每當只要滾輪到底部以後，觸發後收到新的元素加到畫面上，都會發現區塊與區塊之間有白色的間隔，問題找了好久，用firebug發現到，IE8每當我滾輪移到底部時，一般都會觸發一次ajax跟server端要資料，可是IE8卻會一次觸發兩次以上，導致Jquery Masonry計算元素的高度和寬度出現誤差，才會出現空白的間隔

為了改善這個原因，我用比較笨的方式來解決，因為我的功力還沒辦法深入了解瀏覽器間的差異，我發現jQuery ScrollPagination它的範例裡面有用過**stopScrollPagination()**這個方法，看了一下Plugin的原始法，發現它是包覆在外層id名為_container的div，加上一個屬性

	$(obj).attr('scrollPagination', 'disabled');
	
可以用搜尋在jQuery ScrollPagination的原始碼裡面來尋找，所以它利用判別屬性scrollPagination是disabled還是enabled，就可以知道是不是要繼續觸發滾輪事件

我利用了它寫的這段程式碼，來修改一下，在原始碼這段

 	$.fn.scrollPagination.loadContent = function (obj, opts) { ... }
 	
 我在ajax()前面先將scrollPagination屬性先設為disabled，接著在執行完ajax以後，再將屬性設回enabled，讓滾輪事件重新觸發，以下為修改程式碼片段
 
	 $(obj).attr('scrollPagination', 'disabled');
	            $.ajax({
	                type: 'POST',
	                url: opts.contentPage,
	                data: opts.contentData,
	                success: function (data) {
	                    $(obj).append(data);
	                    var objectsRendered = $(obj).children('[rel!=loaded]');
	
	                    if (opts.afterLoad != null) {
	                        opts.afterLoad(objectsRendered);
	                    }
	                    $(obj).attr('scrollPagination', 'enabled');
	                },
	                dataType: 'html'
	            });
	            
其實這有點偷吃步，並不是真正解決核心的問題所在，但無奈底子差，只能先讓程式可以跑(這是重點呀....!)，日後有時間再來好好探討這個問題(其實是希望等著IE8被淘汰的那天...)


以上如有問題或是錯誤的地方，歡迎大家一起討論