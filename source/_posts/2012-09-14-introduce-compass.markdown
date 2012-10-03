---
layout: post
title: "[CSS] 用了就無法回頭的Compass"
date: 2012-09-14 15:24
comments: true
categories: CSS
---

<a href="http://compass-style.org/" target="_blank">Compass</a>這個CSS的framework已經有一陣子了，但我始終沒有去好好了解他，印象中只知道他可以很快的寫出CSS，但可以多快其實我一直無法感受，再加上還要用Ruby的環境，感覺學習曲線就很高，也覺得現在CSS寫的也好好的，就沒多加注意，直到...

<!--more-->

我在看<a href="http://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/css-sprite-sheets-best-practices-tools-and-helpful-applications/">CSS Sprite Sheets: Best Practices, Tools and Helpful Applications</a>這篇文章時，文章尾巴的Tools to Help又提到了Compass，說可以自動生成Sprite，讓我好奇心作祟的打算真正看一下什麼是Compass

沒想到，一用之下，驚為天人！我想這是很多數剛開始接觸Compass的人共同心聲吧，直接來看看怎麼使用吧！

首先要先把Ruby的環境安裝起來，不過因為我是用windows，所以要特別下載<a href="http://www.ruby-lang.org/zh_TW/downloads/" target="_blank">for windows</a>用的，安裝好了以後你可以到Ruby的資料夾底下有個Start Command Prompt with Ruby，開啟命令列，接著安裝Compass

	gem update --system #先更新gem
	gem install compass #安裝Compass
	
安裝完Compass以後，Sass也會自動安裝起來，這邊要稍微提一下甚麼是<a href="http://sass-lang.com/" target="_blank">Sass</a>

**Sass(Syntactically Awesome Stylesheets)**其實就是一個拿來寫CSS樣式表的程式語言，然而還有一個因為CSS3而延伸的語法叫做Scss，兩個寫法有些微的差異，同樣的效果，寫法如下

Scss:

	table.hl {
	  margin: 2em 0;
	  td.ln {
		text-align: right;
	  }
	}

Sass:
	
	table.hl
	  margin: 2em 0
	  td.ln
		text-align: right

可以看到Scss的寫法比較像我們一般看到的CSS，而Sass強調的是更精簡、快速的寫法，所以是利用縮排來呈現

Sass/Scss的特點有可以利用變數，巢狀或是函式和繼承等，至於用法可以參考<a href="http://sass-lang.com/" target="_blank">官網</a>的首頁有簡單的範例，這邊就不提太多

回到Compass，其實Compass也就是一個Sass的Framework，已經把原本要寫很多次的樣式都打包好，剛剛講到安裝完Compass以後現在就來開始使用他

首先建立一個Compass專案

	compass creat mycompass
	
執行成功以後，會看到底下有三個資料夾，一個檔案

	.sass-cache //快取檔案
	sass // sass檔/scss檔
	stylesheets //css檔
	config.rb //設定檔
	
接著你就可以開始編寫Sass檔，除了剛剛說的Sass/Scss的寫法以外，還可以利用Compass強大的功能，例如要做一個reset檔案首先新建一個reset.scss，然後在裡面直接加上以下這段

	@import "compass/reset";

接著可以用compile的方式

	compass compile [資料夾名稱或路徑]
	
或是用監控的方式

	compass watch [資料夾名稱或路徑]
	
我比較喜歡用watch方式，因為這樣改完直接存檔就會自動compile，reset.scss compile以後，就會看到stylesheets資料夾底下就出現reset.css的檔案了！

其他還有像文章開頭提到的自動生成Sprite，到底有多神奇，來看看怎麼做

首先準備兩張圖，一張是facebook的icon，另一張是plurk的icon，如下圖

<img src="https://lh6.googleusercontent.com/-fwPpZzFYl9I/UFL6CnNIZ1I/AAAAAAAABgE/t7FFyDSX-UU/s243/1.jpg" />

接著這邊就是要注意的地方了，一開始我將圖放到icons的資料夾裡面，並且跟sass和stylesheets資料夾都擺在同一層

<img src="https://lh5.googleusercontent.com/-0AQioXIX4X8/UFL6qh2A2SI/AAAAAAAABgM/cuUTLF7UcOs/s660/2.jpg" />

接著我就建一個sprite.scss的檔案並且在裡面加上

	@import "icons/*.png";
	@include all-icons-sprites;  

可是後來發現怎麼compile都沒有用，一直出現以下錯誤訊息

	No files were found in the load path matching "icons/*.png". Your current load
	paths
	
後來我才發現原來在設定檔config.rb裡面有指定圖檔的擺放位置

	http_path = "/"
	css_dir = "stylesheets"
	sass_dir = "sass"
	images_dir = "images" //<--指定圖檔位置
	javascripts_dir = "javascripts"
	
原來是要把icons的資料夾擺在images底下才行，重新指定好位置以後，再一次的compile，就會發現，Compass已經合好圖了！而且連CSS都寫好了！

	.icons-sprite, .icons-facebook, .icons-plurk {
	  background: url('/images/icons-s78250ef0c5.png') no-repeat;
	}

	.icons-facebook {
	  background-position: 0 0;
	}

	.icons-plurk {
	  background-position: 0 -48px;
	}

太強大了！難怪很多人用了都回不去了，因為小弟我也是剛學沒多久，所以還有很多更強大的功能就要請各位自己去發掘了

參考資料:

<a href="http://blog.visioncan.com/2011/compass-sass-your-css/" target="_blank">用強大的compass+sass寫css</a>

<a href="http://kw0006667.wordpress.com/compass-%E2%80%93-%E4%BD%BF%E7%94%A8-ruby-compass-on-windows/" target="_blank">Compass – 使用 Ruby + compass on Windows</a>

如有錯誤，歡迎指正