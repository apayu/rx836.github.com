---
layout: post
title: "[CSS] 做網站非學不可的Twitter Bootstrap"
date: 2012-10-01 18:41
comments: true
categories: CSS jQuery
---

<a href="http://twitter.github.com/bootstrap/" target="_blank">Twitter Bootstrap</a>越來越多人在用了，當然最主要的原因就是他可以幫助網頁開發者快速的開發出，有不錯外觀的web或是mobile apps，這對於許多不擅長外觀設計的網頁工程師們(包括我)，可以說是省下不少煩惱Layout的麻煩，不僅如此，針對按鈕、表格、或是排版，Bootstrap都幫你處理的好好，只要簡單幾個步驟引入即可

<!--more-->

首先要先下載<a href="http://twitter.github.com/bootstrap/getting-started.html" target="_blank">Bootstrap</a>，你可以選擇compil過後的，或是選擇source版本，Bootstrap的css是用Less寫的，所以如果你想修改細節部分，可以下載source版本，一般來說直接用compiled版本即可

接著就會看到有三個資料夾(css & js & img)

<img src="https://lh3.googleusercontent.com/-RHqEXjgftnI/UGl5vs7qyaI/AAAAAAAABoU/tKc440KDt5Y/s872/a.jpg" />

可以把他們全部放入你的專案裡面，但引入到html時，css和js就只要選擇有沒有壓縮過的版本就好

	<!DOCTYPE html>
	<html>
		<head>	
			<meta charset="UTF-8" />
			<title>example</title>
			<link href="css/bootstrap.min.css" rel="stylesheet" type="text/css">		
		</head>
		<body>
			<script src="http://code.jquery.com/jquery-latest.js"></script>
			<script src="js/bootstrap.min.js"></script>		
		</body>
	</html>

然後接下來就可以開始使用了！但請注意還是要引入jQuery喔，接下來就是介紹一些使用範例

## Base CSS examples

### Buttons

加上相對應的class以後，就可以秀出相對應的外觀，例如紅色的按鈕class預設為**btn-danger**，Bootstrap很貼心的讓我們不再只有單調的按鈕顏色
	
	<button class="btn dropdown-toggle" data-toggle="dropdown">Action <span class="caret"></span></button> 
	<button class="btn btn-primary dropdown-toggle" data-toggle="dropdown">Action <span class="caret"></span></button> 
	<button class="btn btn-danger dropdown-toggle" data-toggle="dropdown">Danger <span class="caret"></span></button> 
	<button class="btn btn-warning dropdown-toggle" data-toggle="dropdown">Warning <span class="caret"></span></button> 
	<button class="btn btn-success dropdown-toggle" data-toggle="dropdown">Success <span class="caret"></span></button> 
	<button class="btn btn-info dropdown-toggle" data-toggle="dropdown">Info <span class="caret"></span></button> 
	<button class="btn btn-inverse dropdown-toggle" data-toggle="dropdown">Inverse <span class="caret"></span></button>

<img src="https://lh4.googleusercontent.com/-phDQRFC7UXQ/UGnPIeFHgVI/AAAAAAAABoo/VL2VekJjEVA/s617/123.jpg" />

特別注意的是，按鈕旁邊有個倒三角形是用css做出來的，也同樣只要在span加一個class為caret即可

### Progress bars

進度條只要外面包一層div給予相對的class，裡面再加一個div並且命名class為**bar**，**width**就是進度條的長度，這樣就可以用js來修改width顯示目前的進度狀況

	<div class="progress progress-info" style="margin-bottom: 9px;"> <div class="bar" style="width: 10%"></div> </div> 
	<div class="progress progress-success" style="margin-bottom: 9px;"> <div class="bar" style="width: 20%"></div> </div> 
	<div class="progress progress-warning" style="margin-bottom: 9px;"> <div class="bar" style="width: 30%"></div> </div> 
	<div class="progress progress-danger" style="margin-bottom: 9px;"> <div class="bar" style="width: 40%"></div> </div>
	
<img src="https://lh6.googleusercontent.com/-CWMKYBHmiBk/UGpPoPagCQI/AAAAAAAABo8/o7uycvmJotE/s926/123.jpg" />

更酷的是，bar的樣式也可以更改，而不是只有醜醜的實心bar

	<div class="progress progress-striped active"> 
	<div class="bar" style="width: 40%;"></div> 
	</div>
	
只要修改class為**progress progress-striped active**，就會有條紋的進度條，而且還加上css3的animation動畫

### Button groups

也可以將button設為一組群組，就會有群組的樣式

	<div class="btn-group" style="margin: 9px 0;"> 
	<button class="btn">Left</button> 
	<button class="btn">Middle</button> 
	<button class="btn">Right</button> 
	</div>

<img src="https://lh4.googleusercontent.com/-iCtFSRwd7UU/UGpYAp2xh6I/AAAAAAAABpQ/BVql_Jk9oto/s187/4.jpg" />
	
用一個class名為**btn-group**的div包住button就可以

### Horizontal and vertical tabs (with dropdown menus)

還在煩惱下拉選單嗎?

	<ul class="nav nav-tabs"> 
	<li class="active"><a href="#">Home</a></li> 
	<li><a href="#">Portfolio</a></li> 
	<li class="dropdown"> <a class="dropdown-toggle" data-toggle="dropdown" href="#">Services <b class="caret"></b></a> 
	<ul class="dropdown-menu"> <li><a href="#">Link 1</a></li> 
	<li><a href="#">Link 2</a></li> 
	</ul> </li> 
	</ul>
	
只要用ul li包好，並且加上相對應的class，就可以輕鬆做tab+下拉選單

<img src="https://lh5.googleusercontent.com/-ix3_DDLLdWg/UGpZ2cBhygI/AAAAAAAABpY/wzbaSwCDMb8/s303/5.jpg" />


### Navigation bar component

看到這邊就覺得實在太強大了...

	<div class="navbar"> 
		<div class="navbar-inner"> 
			<div class="container"> <!-- brand class is from bootstrap.css --> 
				<a class="brand" href="#">My Brand</a> 
				<div class="nav-collapse"> 
					<ul class="nav"> 
						<li class="active"><a href="#">Home</a></li> 
						<li><a href="#">Services</a></li> 
						<li class="dropdown"> <a href="#" class="dropdown-toggle" data-toggle="dropdown">Dropdown <b class="caret"></b></a> 
							<ul class="dropdown-menu"> 
								<li><a href="#">Action 1</a></li> 
								<li><a href="#">Action 2</a></li> 
								<li class="divider"></li> 
								<li class="nav-header">Header</li> 
								<li><a href="#">Separated action</a></li> 
							</ul> 
						</li> 
					</ul> 
					<form class="navbar-search pull-left"> 
					<input type="text" class="search-query" placeholder="Search"> 
					</form> 
				</div><!-- /.nav-collapse --> 
			</div> 
		</div><!-- /navbar-inner --> 
	</div><!-- /navbar -->
		
<img src="https://lh5.googleusercontent.com/-VBBWEKhYfzk/UGpba2H2VSI/AAAAAAAABpg/2KVa_kC0xX0/s647/6.jpg" />

### Using the layout and built-in grid system 

你也可以用他們的grid system

	<div class="container"> 
		<div class="row"> 
			<div class="span4"> <!--content--> </div> 
			<div class="span4"> <!--content--> </div> 
			<div class="span4"> <!--content--> </div> 
		</div> 
	</div>
	
預設是 12-column，940 pixel-centered layout

### Responsive design

連最近很紅的responsive design也有，只要引入他們的**bootstrap-responsive.css**這個css檔案


### Typeahead example

裡面也有plugin可以使用，例如下拉提示選單

	<input type="text" class="span3" style="margin: 0 auto;" 
	data-provide="typeahead" 
	data-items="4" 
	data-source='["Apples","Bananas","Cherries","Dates","Eggplants","Figs","Grapes", "Honeydew","Kiwi","Mango","Peaches","Plums","Raspberries","Strawberries","Watermelon","Zucchini"]'>
	
<img src="https://lh6.googleusercontent.com/-y8ELDPfXQp4/UGpdfcl99uI/AAAAAAAABpo/A_l1HiZDL2I/s223/7.jpg" />


還有很多使用範例，可以直接去<a href="http://twitter.github.com/bootstrap/index.html" target="_blank">官網看</a>，這樣大概看了一下教學範例，一個網站可能需要的元素，Bootstrap幾乎通通都有，網頁開發人員可以更專注在開發網頁這個事情上面

只是不知道，會不會到後來，大家的網站都長得很像:)

參考資料:

<a href="http://www.adobe.com/devnet/html5/articles/twitter-bootstrap.html" target="_blank">Styling your apps with Twitter Bootstrap </a>

<a href="http://www.w3resource.com/twitter-bootstrap/tutorial.php" target="_blank">Twitter Bootstrap tutorial</a>

<a href="http://twitter.github.com/bootstrap/index.html" target="_blank">Twitter Bootstrap</a>

如有錯誤，歡迎指正

