---
layout: post
title: "[CSS] 拋棄原生checkbox用CSS3自己簡單動手做"
date: 2012-11-16 15:27
comments: true
categories: CSS
---

<img src="https://lh5.googleusercontent.com/-AstthsAdcVk/UKX5J1b1PpI/AAAAAAAAB7U/UxqFI-iYi0g/s166/a.jpg" />

已經用膩原生的checkbox和radiobutton嗎？今天就試著用CSS3來做出不一樣的checkbox和radiobutton吧，而且是不用任何一行JavaScript，重點是，就算IE9以下不支援CSS3也沒關係喔！

<!--more-->

在開始之前，先認識一下什麼是 <a href="http://meyerweb.com/eric/articles/webrev/200007a.html" target="_blank">Adjacent-Sibling Selector</a>，這等下會用到，簡單的範例如下

HTML
	<div>
		<span></span>
		<p>apa</p>
	</div>
	
CSS

	span + p{
		color:red;
	}
	
可以看到這樣寫「apa」就會顯示紅色，「+」的用法就是等於選擇兄弟元素的意思

OK，那我們要怎麼做出不一樣的checkbox和radiobutton呢？先建立HTML部分吧
	
	<input type="checkbox" />
	<label>Check Box 1</label>
	
會用label的原因是希望可以在點擊「Check Box 1」也可以選擇checkbox，讓**可點擊的範圍**更大，所以為了有這個效果，我們就需要用到label的屬性「for」

	<input type="checkbox" id="c1" name="cc" />
	<label for="c1">Check Box 1</label>
	
會看到for指定的id為input #c1

再來我們可以在label裡面放一個span，為的就是等下可以直接在span加上背景圖，當然你也可以不用span而直接在label放背景圖，不過這樣當調整位置的時候會比較不方便，所以跟放文字的label分開會比較好

	<input type="checkbox" id="c1" name="cc" />
	<label for="c1"><span></span>Check Box 1</label>

接著是CSS部分，首先為了替換掉原生的HTML樣式，我們先將原生的checkbox隱藏起來

	input[type="checkbox"] {
		display:none;
	}
	
這邊要特別注意的是，雖然看不到checkbox，實際上他還是存在喔！一樣還是會有勾選效果，只是看不到而已，隱藏完以後，我們就要將背景圖設置到span裡面

	input[type="checkbox"] {
		display:none;
	}
	input[type="checkbox"] + label span {
		display:inline-block;
		width:19px;
		height:19px;
		background:url(check_radio_sheet.png) left top no-repeat;
	}
	
有看到選擇器「input[type="checkbox"] + label span」這樣的寫法嗎？這就是之前講的選擇兄弟元素

那圖的部分就可以用CSS Sprite的方式來呈現，把需要的小icon放在同一張圖，利用位移來顯示出想要的部分，將其它不要的部分隱藏0

<img src="https://lh5.googleusercontent.com/-VSnKVuXA5k4/UKX5J-71RvI/AAAAAAAAB7Q/hDmvr5xxMjg/s76/check_radio_sheet.png" />
	
最後，剛剛那個是「尚未選取」的CSS狀態，這邊就把「選取後」的CSS狀態也一併加上吧，也就是CSS3的「:checked」

	input[type="checkbox"] {
		display:none;
	}
	input[type="checkbox"] + label span {
		display:inline-block;
		width:19px;
		height:19px;
		margin:-1px 4px 0 0;
		vertical-align:middle;
		background:url(check_radio_sheet.png) left top no-repeat;
		cursor:pointer;
	}
	input[type="checkbox"]:checked + label span {
		background:url(check_radio_sheet.png) -19px top no-repeat;
	}
	
大功告成！很簡單吧？而且不用任何一行JavaScript

原理其實就是將原生的checkbox隱藏起來，再利用CSS的選擇器「:checked」來分辨checkbox目前的狀態(是否選取)，然後換掉相對應的span背景圖，如果不太懂的話，可以先暫時把「display:none」就會比較明瞭囉

### IE9以下不支援CSS3怎麼辦呢？

不用擔心，這種做法有個好處就是向下兼容，就算沒有支援CSS3，頂多就是恢復到以前原生的樣式，並不會影響使用者喔！

<img src="https://lh4.googleusercontent.com/-Uyji0CjOhRU/UKX61r2rp9I/AAAAAAAAB7g/2rQS4EpXUBI/s171/VASV.jpg" />


參考資料:

<a href="http://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/quick-tip-easy-css3-checkboxes-and-radio-buttons/" target="_blank">Quick Tip: Easy CSS3 Checkboxes and Radio Buttons</a>

<a href="http://www.w3.org/TR/CSS2/selector.html#adjacent-selectors" target="_blank">Selectors</a>

內容如有錯誤，歡迎指正
