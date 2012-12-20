---
layout: post
title: "[jQ-Plugin] 輕鬆加入Tag標籤功能的plugin-Tags Manager"
date: 2012-12-20 11:11
comments: true
categories: jQ-Plugin
---

<img src="https://lh5.googleusercontent.com/-gxsgoBxzDI8/UNKSYvcQnPI/AAAAAAAACFc/7PiDy2u-3KA/s745/2012-12-20_111514.jpg" />

如果有在 <a href="http://stackoverflow.com/" target="_blank">stackoverflow</a> 上找過答案的朋友，應該對於他們的tag並不陌生，類似這樣的功能在許多blog或是論壇都有，但光是只有Tag這個功能已經不是重點所在，如何讓User有良好的Tag經驗是現今大家所追求的，簡單的說就是使用者經驗(UX)，今天就來介紹一款我個人覺得不錯的jQuery plugin - Tags Manager

<!--more-->

##Start

<a href="https://github.com/max-favilli/tagmanager" target="_blank">Download from Github</a>

使用方式相當相當的簡單，從github載下來後，將Tags Manager和所需要的css檔案掛載到網頁裡面，接下來只有兩個步驟

第一步驟就是在html裡面加上一個&lt;input&gt;

	<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
	
第二個步驟就是在js加上一段程式碼

	jQuery(".tagManager").tagsManager();
	
完成，本篇介紹到此結束

.

.

.

.

好啦，真的就只有這兩行，打開網頁後你可以看到會有一個input，裡面有個預設文字Tags

<img src="https://lh5.googleusercontent.com/-OR2B3B8UzXs/UNKSYj723cI/AAAAAAAACFg/Pz1flQNbeKg/s149/2012-12-20_113137.jpg" />

接著你在裡面輸入文字，只要**你的焦點離開input**、**按下Enter**或是**加上逗號**，都會自動幫你生成一個Tag

<img src="https://lh5.googleusercontent.com/-Rq7wFJw2IH4/UNKSYmV6tWI/AAAAAAAACFk/k9e3c11qyZg/s202/2012-12-20_113346.jpg" />

而假如要刪除呢？只要對著Tag裡面的小x按下即可，這對於使用者來說非常的方便使用，那對於開發者來說要如何操作呢？

也許會有人問那我要怎麼取得那些Tag的值，如果你有用firebug或是google Chrome(按下F12呼叫開發者環境)，可以看到Tags Manager會在增加Tag的同時，默默的在背後新增一個hidden，並且把值丟到裡面做暫存，所以當開發者想要將Tag的值送到Server端時，可以從這裡取出

<img src="https://lh4.googleusercontent.com/-hfXPhL3aF1g/UNKSZaCL9fI/AAAAAAAACFo/aKDNo-6VMj8/s658/2012-12-20_113905.jpg" />

當然，Tag裡面還有很重要的一個功能就是智能輸入，會出現關鍵字的提示，但因為Tags Manager是利用 <a href="http://twitter.github.com/bootstrap/index.html" target="_blank">Bootstrap</a> 裡面的 <a href="http://twitter.github.com/bootstrap/javascript.html#typeahead" target="_blank">typeahead</a> ，所以要用到關鍵字的提示要載入Bootstrap才可以使用，以下就是範例

	jQuery(".tagManager").tagsManager({
		prefilled: ["Pisa", "Rome"],
		typeahead: true,
		typeaheadSource: funSource
	});
	
	function funSource(){
		var ret = ["Manchester", "Astonvilla", "Real Madrid", "Barcelona", "Milan AC", "Internazionale", "Roma AC", "Chelsea"];
		return ret;
	} 
	
你可以將需要提示的tag寫成一個陣列，將值塞入參數 **typeaheadSource**

其他的參數分別為

<ul>
<li>prefilled:預先給予的Tag</li>
<li>CapitalizeFirstLetter:如果為true，會將Tag第一個字轉為大寫，其他為小寫</li>
<li>preventSubmitOnEnter:如果為true，假設&lt;input&gt;在&lt;form&gt;裡面，按下Enter將不會觸發Sibmit</li>
<li>typeahead:如果為true，就會有關鍵字的提示選擇</li>
<li>typeaheadAjaxSource:可以從Server端接收JSON格式的關鍵字提示選擇</li>
<li>typeaheadSource:可以接收陣列或funtion回傳陣列的關鍵字提示選擇</li>
</ul>

這邊只介紹幾個主要的參數，其他還有許多不錯的參數應用可以直接參考 <a href="http://welldonethings.com/tags/manager" target="_blank">Tags Manager</a>

##總結

這是一套蠻方便的plugin，對於他的樣式如果不太喜歡還可以自己進行修改，另外對Tag還想要有更多的其他選擇，也可以參考 <a href="http://ioncache.github.com/Tag-Handler/" target="_blank">Tag Handler</a>、<a href="http://xoxco.com/projects/code/tagsinput/" target="_blank">jQuery Tags Input Plugin</a> 這些參考文章

###參考資料:

<a href="http://welldonethings.com/tags/manager" target="_blank">Tags Manager (a jQuery plugin)</a>

內容如有錯誤，歡迎指正
