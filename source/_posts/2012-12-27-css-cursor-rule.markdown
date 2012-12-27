---
layout: post
title: "[CSS] 關於CSS Cursor"
date: 2012-12-27 15:09
comments: true
categories: CSS
---

<img src="https://lh5.googleusercontent.com/-OVdRqH4Q_sA/UNwXOft01eI/AAAAAAAACH4/Kg-eysHdgc8/s461/2012-12-27_152249.jpg" />

在提到CSS Cursor之前，要先說一下我跟CSS Cursor的第一次的認識，在我剛出社會時，做活動網站，常常會使用&lt;div&gt;來當作button來使用，有一天，PM跑過來跟我說，要把那個按鈕的鼠標從箭頭改成指頭，我才了解到鼠標對User的影響

<!--more-->

##Cursor

先來簡單的介紹鼠標的作用，鼠標其實就是輔助你讓你知道現在可以做些甚麼事情，例如當你將滑鼠移到視窗邊緣時，會出現可以**縮放的標誌**，又或是將鼠標移到文字框時，會出現類似「工」型的圖案，意思是你可以在這邊輸入文字

<img src="https://lh5.googleusercontent.com/-RdOW3VCBij4/UNwXOavbpLI/AAAAAAAACH8/JaDJMEYNyzM/s600/cursor_inputs.png" />

這在不管是系統的應用程式上，或是網頁瀏覽時，都是很常看到的輔助標誌，但我們今天主要講的是網頁瀏覽時的鼠標應用，在CSS裡面，如果要更改預設的鼠標，語法會是這樣寫

	div{
		cursor:move;
	}
	
**cursor** 是屬性名稱，而 **move** 是屬性值，當然，屬性值不只有move可以使用，更多的屬性值可以參考下面那個網站，也是我本人相當推薦的參考網站

<a href="http://webdesigntutsplus.s3.amazonaws.com/tuts/405_cursors/table/table.html" target="_blank">CSS Cursor Values Across Browsers and Platforms</a>

看過上面那個網站，會發現到，除了瀏覽器的不同以外，就連User所使用的系統不同，也會有不同的結果

那假如不想使用上面那些預設的圖案呢？我有沒有辦法使用自訂的鼠標？答案是有的，語法如下

	div{
		cursor: url('cursor.png'), default;
	}
	
它跟 **font-family** 一樣，都需要有備用的鼠標，假如第一個鼠標不存在或不支援時，還能使用其它鼠標

也可以加上自訂圖案的位移座標

	cursor: url('cursor.png') 10 5, default;
	
分別代表x和y，用原始鼠標為起點(0,0)，往左位移10px，往上位移5px

##Cross Browser Cursor Rule

不過要做到跨瀏覽器有幾點要特別注意的是，IE7、8只支援 **.CUR** 的檔案，所以一般我們都會這樣寫

	div{
		cursor: url('/cursors/cursor.png'),
					url('/cursors/cursor.cur'),
					default;
	}		

讓非IE的瀏覽器使用第一個.png圖檔，假如是IE就使用.cur圖檔，都無法讀取時就使用default

特別注意的是，假如你的cursor圖檔與css檔是放在不同資料夾的話，IE的CSS Cursor**並不支援相對路徑**，只支援**相對根路徑**或是**絕對路徑**，所以像下面的寫法IE是不支援的

	cursor: url(../cursors/cursor.cur);
	
##結論

現在利用移動設備瀏覽網頁的使用程度上越來越高，觸控式的螢幕輸入占了絕大多數，可能會覺得鼠標的影響已經越來越不重要，但不管如何，除非傳統的web網頁消失，不然建議大家還是要照著Progressive Enhancement(漸進式增強)的原則來設計網頁，達到良好的互動式設計
				
###參考資料:

<a href="http://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/everything-you-need-to-know-about-the-css-cursor-rule/?utm_source=CSS+Weekly&utm_campaign=CSS_Weekly_Issue_34&utm_medium=web" target="_blank">Everything You Need to Know About the CSS Cursor Rule</a>

<a href="http://abgne.tw/css/css-mouse-cursor.html" target="_blank">男丁格爾-自訂網頁中的滑鼠游標</a>

<a href="http://hi.baidu.com/guohuihot/item/c88f6af387dcaec2a835a223" target="_blank">IE不支持CSS相对路径的自定义cursor</a>

內容如有錯誤，歡迎指正
