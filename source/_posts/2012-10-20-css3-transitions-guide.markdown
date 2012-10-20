---
layout: post
title: "[CSS3] 認識CSS3 transitions"
date: 2012-10-20 23:24
comments: true
categories: CSS
---

一直沒有找個時間好好的了解一下CSS3 transitions，趁著看到<a href="http://www.adobe.com/devnet/html5/articles/using-css3-transitions-a-comprehensive-guide.html" target="_blank">這篇</a>文章，就來筆記一下用法，扎實一下基本功

<!--more-->

CSS3 transitions可以改變css屬性的值，在某個期間內做出變化，類似<a href="http://api.jquery.com/animate/" target="_blank">jQuery.animate()</a>，語法結構如下

	.example {     
		transition-property: background-color;     
		transition-duration: 2s;     
		transition-timing-function: ease-in;     		
		transition-delay: 1s; 
	}
	
這裡沒有特別加上prefixes，在真正使用的時候要自行加上，接著是分別講解每個屬性的用途

**transition-property:** 指定你要變化的CSS屬性，至於哪些屬性是擁有transition效果可以查看<a href="http://www.w3.org/TR/css3-transitions/#animatable-properties" target="_blank">這張表</a>

**transition-duration:** 指定transition從開始到結束的變化時間，在數字後面加上s就是以秒計算，用ms就是微秒

**transition-timing-function:** 根據時間的進行去改變屬性值的變化速率，也就是貝茲曲線，詳細的介紹可以參考<a href="http://www.w3.org/TR/css3-transitions/#transition-timing-function-property" target="_blank">這篇</a>，基本的有linear, ease-in, ease-out和ease-in-out這些值可以使用

**transition-delay:** 可以指定秒或微秒來延遲transition觸發的時間

### Transition shorthand

為了簡潔也可以這樣寫

	.example {     
		transition: background-color 2s ease-in 1s; 
	} 
	
要特別注意的是，順序的重要性，另外第一個時間代表是**transition-duration**，第二個時間是**transition-delay**，如果你要定義**transition-delay**一定要先定義**transition-duration**才行

### Multiple transitions

如果想在同個元素上定義複數個transitions，可以用下面寫法

	.example {     
		transition:  background-color  2s ease-in 1s,      
		width  2s ease-in-out,      
		height 3s ease-out; 
	}
	
記得要用**逗號**隔開

### Triggering a transition

但其實光寫上面那些語法並不能實現transitions，原因在於沒有**觸發**這個動作，所以我們可能要加些"動作"，例如比較常見的是**:hover**

	.example {     
		background-color: green;     
		transition: background-color  2s ease-in 1s; 
		width:100px;
        height:100px;  
	} 
	.example:hover {     
		background-color: blue 
	}
	
<a href="http://jsfiddle.net/Pa5Uk/1/" target="_blank">範例</a>

會看到如果將滑鼠移到div .example上面，會先等待一秒，接著再花兩秒的時間從綠色轉換成藍色

### Transitions triggered by JavaScript 

假如要搭配JavaScript呢？我們可以使用jQuery來示範一下

css

	.example {     
        background-color: green;     
        transition: background-color  2s ease-in 1s;
        width:100px;
        height:100px;  
    }
    .style-change {     
        background-color: blue
    }
	
html

	<div id="a" class="example"></div>
	
js

	$("#a").click(function() {         
		$(".example").toggleClass("style-change");    
	}); 
	
<a href="http://jsfiddle.net/Rnebd/" target="_blank">範例</a>

這樣就可以搭配著js來使用transition的效果

### Transition tricks and techniques 

有了前面的一些基本用法以外，接下來介紹的是一些小技巧，前面的**:hover**例子不管是從綠色切換成藍色，還是藍色切換回綠色，都是同樣的效果和速度，但其實可以針對這兩者去做變化，例如

	.example {     
        background-color: green;     
        transition: background-color  1s ease-out;
        width:100px;
        height:100px;    
    }
    .example:hover {     
        background-color: blue;
        transition: background-color  5s linear;
    }
	
這段意思是從綠色到藍色要花一秒的時間，但從藍色變回綠色要花五秒，就可以做出比較不一樣的效果

	.example {     
		width: 100px;     
		height: 100px;     
		background-color: blue;     
		transition: width 0s ease-out 999999s,                 
		height 0s ease-out 999999s; } 
		
	.example:active {     
		width: 200px;     
		height: 200px;     
		transition: width 2s,                 
		height 2s; 
	}
	
當然也可以把transition-delay設為999999s，這樣就可以將效果一直保存

只是我目前還不知道這樣的保存可以用來做啥就是了...

參考資料:

<a href="http://www.adobe.com/devnet/html5/articles/using-css3-transitions-a-comprehensive-guide.html" target="_blank">Using CSS3 transitions: A comprehensive guide</a>

<a href="http://www.w3cplus.com/content/css3-transition" target="_blank">CSS3 Transition</a>

內容如有錯誤，歡迎指正