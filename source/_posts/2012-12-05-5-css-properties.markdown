---
layout: post
title: "[CSS] 5個對設計師有幫助的CSS屬性"
date: 2012-12-05 14:50
comments: true
categories: CSS
---

如果要寫一個網頁，基本上就是利用HTML+CSS互相搭配(廢話)，網路上的教學也非常的多，除非是剛踏入這一行的新手，不然大部分的人對這都不陌生，不過雖然CSS整體來說並不難，但有幾個特別的屬性他並不是這麼直覺好懂，但卻很適合設計師來學習，所以這篇就來筆記幾個CSS，來幫助釐清觀念

<!--more-->

##Clear

首先來看一個基本的網站架構

HTML

	<div id="container">
		<h1>網站標題</h1>
		<div id="content">
			<h2>文章標題</h2>
			<p>文章內容文章內容文章內容文章內容文章內容文章內容文章內容文章內容文章內容文章內容</p>
		</div>
		<div id="sidebar">
			<h2>側邊欄位1</h2>
		</div>
		<div id="sidebar2">
			<h2>側邊欄位2</h2>
		</div>
		<div id="footer">我是footer</div>
	</div>
	
CSS

	#container{
		background:#0CF;
		width:450px;
	}
	#content{
		background:#FC3;
		width:250px;
		float:left;
	}
	#sidebar{
		float:left;
		background:#360;
		width:100px;
	}
	#sidebar2{
		float:left;
		background:#F0F;
		width:100px;
	}
	#footer{
		
	}
	
看起來就長的像這樣

<img src="https://lh6.googleusercontent.com/-hrlyAdCFVM4/UL9zdLc_WSI/AAAAAAAACBY/obrq-cebCvY/s470/2012-12-05_225116.jpg" />
	
HTML部份就是利用一個div做為最外層的container，裡面包有content、sidebar和footer，利用CSS的屬性 **float**，將content和sidebar排成水平一直線，這是排版常使用的技巧，可是會發現，footer卻不是心中所想的那樣置底，反而受到float影響而圍繞在其他的div周圍

###如何讓單一的div消除float的影響

就是 **Clear** 的功效，所以為了讓footer排在應該有的位置，我們可以這樣添加CSS屬性

	#footer{
		clear:both;
	}
	
結果

<img src="https://lh6.googleusercontent.com/-j2gYazTo_HE/UL9zdAr8LVI/AAAAAAAACBg/EN-h4zoISdQ/s466/2012-12-05_230147.jpg" />

有發現了嗎？只要簡單的加上clear這個屬性，div就會乖乖地恢復他本來的特性，讓你水平或垂直排列可以隨心所欲

##Box Shadows

box-shadow這個新的CSS3屬性之前有在<a href="http://blog.rx836.tw/blog/css3-real-beauty-box-shadows/" target="_blank">文章</a>介紹過，其實他就是利用CSS很方便的做出陰影效果，例如像這樣加上CSS

	#content{
		background:#ccc;
		width:250px;
		float:left;
		padding:5px;
		-webkit-box-shadow: inset 0px 0px 2px 2px #f00;
		box-shadow: inset 0px 0px 2px 2px #f00;
	}
	
我們這邊利用box-shadow做出有內嵌效果的div，並且加上5px的內距，會發現整個網站會長成這樣

<img src="https://lh5.googleusercontent.com/-dxl0B5r8Ksk/UL9zdMMiRLI/AAAAAAAACBc/lGKF0VdvFo8/s469/2012-12-05_231526.jpg" />

這也是寫CSS常會發生的事情，一個沒注意就破版了，原因是之前設container寬度為450px，content為250px，兩個sidebar分別為100px，這樣加起來是剛好的，但加上了padding的5px以後(有左右兩邊，所以實際是10px)，兩個sidebar必須調整為95，這樣才不會擠壓到

	#sidebar{
		float:left;
		background:#360;
		width:95px;
	}
	#sidebar2{
		float:left;
		background:#F0F;
		width:95px;
	}
	
<img src="https://lh5.googleusercontent.com/-S0FvavMd3Lo/UL9zdySksMI/AAAAAAAACBk/DnzWTwuLljo/s468/2012-12-05_232026.jpg" />
	
這樣就正常了，回到剛剛的box-shadow，可以看到為了跨瀏覽器的關係，我們在使用box-shadow會搭配每個瀏覽器的前綴

	-webkit-box-shadow: inset 0px 0px 2px 2px #f00;
	
另外box-shadow屬性寫法如下

	box-shadow: inset x-offset y-offset blur spread color
	
每個值所代表的意義為

**x-offset**: 水平位移植，必須要指定

**y-offset**: 垂直位移植，必須要指定

**blur**: 模糊效果，不能為負值，預設為0

**spread**: 擴散強度，可以為負值(縮小)，預設為0

**color**: 顏色，有些網站可能會寫預設值為黑色，**但一般建議還是要給予顏色，因為有些瀏覽器預設值並不一定為黑色(例如手機)**

**inset**: 這個值有些人是放在**最前面**，有些是放在**最後面**，兩者皆可，如果有給予這個值box就會在陰影裡面，反之則在外面
	
而除了box-shadow以外，CSS3其實還有針對文字的text-shadow，範例如下

	h2{
		Font-family:"Palatino Linotype", "Book Antiqua", Palatino, serif;
		color:#fff;
		text-shadow: -2px 0px 3px #003366;
	}
	
差別在於text-shadow沒有spread，而效果看起來就像這樣

<img src="https://lh5.googleusercontent.com/-2vCt4XwlUoY/UL9zeNS-J5I/AAAAAAAACBo/TMv2Oo5TPAg/s469/2012-12-05_233015.jpg" />

明顯可以看出文字擁有立體的感覺

##CSS Gradients

用CSS3來表達漸層，用法其實不難，難的是要做到跨瀏覽器不是一件很容易的事情，以下是範例語法

	#container{
		background: #a8e7ff; /* Old browsers */
		background: -moz-linear-gradient(top,  #a8e7ff 0%, #4096ee 100%); /* FF3.6+ */
		background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#a8e7ff), color-stop(100%,#4096ee)); /* Chrome,Safari4+ */
		background: -webkit-linear-gradient(top,  #a8e7ff 0%,#4096ee 100%); /* Chrome10+,Safari5.1+ */
		background: -o-linear-gradient(top,  #a8e7ff 0%,#4096ee 100%); /* Opera 11.10+ */
		background: -ms-linear-gradient(top,  #a8e7ff 0%,#4096ee 100%); /* IE10+ */
		background: linear-gradient(to bottom,  #a8e7ff 0%,#4096ee 100%); /* W3C */
		filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#a8e7ff', endColorstr='#4096ee',GradientType=0 ); /* IE6-9 */
	}
	
<img src="https://lh4.googleusercontent.com/-HaSJlf5Trxc/UL9zec5QzcI/AAAAAAAACBs/ewEGX4ImfBc/s605/2012-12-05_233546.jpg" />

可以看到頁面從淡藍變成深藍，而且是用CSS而不是圖片來達成，但為了配合到每個瀏覽器這裡使用了8行的CSS，每一行的CSS都長的不太一樣，這也是比較令人煩惱的地方，基本的語法如下

	(top,  #a8e7ff 0%,#4096ee 100%)
	
這意思就是指漸層的效果是從最上方開始變化到最下方，如果是50%，就是指從中間開始

##Dropdown Menus

下拉選單是網站常見的元素，可以利用HTML加上CSS來呈現這樣的效果，關鍵點在於 **hover** 和 **display:none**，範例如下

HTML

	<div class="menubar">
	<ul>
		<li><a href="#" >Home</a></li>
		<li><a href="#" id="current">Products</a>
			<ul> <li><a href="#">Sliders</a></li>
			<li><a href="#">Galleries</a></li>
			<li><a href="#">Apps</a></li>
			<li><a href="#">Extensions</a></li>
			</ul>
		</li>
		<li><a href="/about.html">About</a> </li>
		<li><a href="#">Company History</a></li>
		<li><a href="#">Address</a></li>
		<li><a href="#">Customer Service</a></li>
		<li><a href="#">Contact</a></li>
	</ul>
	</div>
	
CSS

	.menubar{
		border:none;
		border:0px;
		margin:0px;
		padding:0px;
		font: 67.5% "Lucida Sans Unicode", "Bitstream Vera Sans", "Trebuchet Unicode MS", "Lucida Grande", Verdana, Helvetica, sans-serif;
		font-size:14px;
		font-weight:bold;
	}
	.menubar ul{
		background: rgb(109,109,109);
		height:50px;
		list-style:none;
		margin:0;
		padding:0;
	}
	.menubar li{
		float:left;
		padding:0px;
	}
	.menubar li a{
		background: rgb(109,109,109);
		color:#cccccc;
		display:block;
		font-weight:normal;
		line-height:50px;
		margin:0px;
		padding:0px 25px;
		text-align:center;
		text-decoration:none;
	}
	.menubar li a:hover, .menubar ul li:hover a{
		background: rgb(71,71,71);
		color:#FFFFFF;
		text-decoration:none;
	}
	.menubar li ul{
		background: rgb(109,109,109);
		display:none;
		height:auto;
		padding:0px;
		margin:0px;
		border:0px;
		position:absolute;
		width:200px;
		z-index:200;
		/*top:1em;
		/*left:0;*/
	}
	.menubar li:hover ul{
		display:block;
	}
	.menubar li li {
		background: rgb(109,109,109);
		display:block;
		float:none;
		margin:0px;
		padding:0px;
		width:200px;
	}
	.menubar li:hover li a{
		background:none;
	}
	.menubar li ul a{
		display:block;
		height:50px;
		font-size:12px;
		font-style:normal;
		margin:0px;
		padding:0px 10px 0px 15px;
		text-align:left;
	}
	.menubar li ul a:hover, .menubar li ul li:hover a{
		background: rgb(71,71,71);
		border:0px;
		color:#ffffff;
		text-decoration:none;
	}
	.menubar p{
		clear:left;
	}
	
看起來的效果就像這樣

<img src="https://lh4.googleusercontent.com/-bnIvT8x3nww/UL9ze-1MTWI/AAAAAAAACB8/c4k6lL2dy_k/s896/2012-12-05_235741.jpg" />

不用任何一行js就可以做出下拉的選單，而剛剛提到的關鍵點屬性display

	.menubar li:hover ul{
		display:block;
	}
	
利用這個屬性就可以做到將滑鼠移過去的時候，子選單就會呈現出來

##Border Radius

**圓角**也是做網站設計很常用到的元素，利用CSS3的屬性border-radius也可以輕鬆做到，但有些人或許不知道圓角還可以針對四個角做不同的設置，範例如下

CSS

	#container{
		background: #a8e7ff; /* Old browsers */
		width:600px;
		-webkit-border-radius: 20px 5px 115px 35px;
		border-radius: 20px 5px 115px 35px;
	}

我們一樣拿剛剛最前面那個範例來說明，效果如下

<img src="https://lh3.googleusercontent.com/-xzuDA1ptHRo/UL9zfIUb32I/AAAAAAAACB4/cKv2qf7ahQM/s619/2012-12-06_001054.jpg" />

可以看到四個角給的值不同，圓角的效果也都不同，但特別注意的是，在使用圓角效果時，要注意會不會有破版的情形發生，就如同圖的左下角圓角，跟剛剛提到的padding意思一樣

以上是幾個對設計師來說好用的CSS屬性，希望對大家有幫助

###參考資料:

<a href="http://designfestival.com/5-css-properties-that-give-designers-fits/" target="_blank">5 CSS Properties That Give Designers Fits</a>

內容如有錯誤，歡迎指正