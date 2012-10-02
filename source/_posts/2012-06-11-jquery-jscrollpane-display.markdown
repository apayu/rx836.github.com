---
layout: post
title: "[jQuery] jScrollPane的使用與注意"
date: 2012-06-11 18:26
comments: true
categories: 
---
有些時候客戶會不想要HTML內建的Scrollbar，所以特地去找了一個Jquery Plugin來使用，但注意，如果有使用到display:none，或是類似lightbox視窗效果，要注意一下先後執行的問題

<!--more-->

當然，還有其他很多Plugin可以選擇<a href="http://www.net-kit.com/jquery-custom-scrollbar-plugins/" target="_blank">10 jQuery Custom Scrollbar Plugins</a>，這裡我是用jScrollPane，使用方法很簡單，先下載他的檔案回來，在載入到網頁

使用方法

	<!-- CSS部分 -->
	<link type="text/css" href="style/jquery.jscrollpane.css" rel="stylesheet" media="all" />

	<!-- 還要載入Jquery 這裡用CDN -->
	<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.4.2/jquery.min.js">
	</script>

	<!-- 載入mousewheel plugin -->
	<script type="text/javascript" src="script/jquery.mousewheel.js"></script>

	<!-- 載入jScrollPane -->
	<script type="text/javascript" src="script/jquery.jscrollpane.min.js"></script>
	
接著只要對包覆內容的div加上Jquery語法

	$(function()
	{
		$('.your div').jScrollPane();
	});
	
這樣就可以自製Scrollbar了！很簡單吧

這裡有<a href="http://jscrollpane.kelvinluck.com/#examples" target="_blank">更多範例</a>

不過有時候我們會遇到一個狀況，一開始會設div為display:none，然後點了某個元件以後，用lightbox或其他方式秀出div，如下圖

<img width="300px" src="https://lh4.googleusercontent.com/-NBEVwEqZHlY/T9XCoGfeq1I/AAAAAAAAAQc/sWHyCp2vi6M/w753-h585-k/a.jpg" />

但會發現，依照正常流程來套用，點開呈現的效果不如預期，那是因為你在還沒套用jScrollPane之前，為了呈現lightbox的效果，就已經先將他display:none，為了避免發生這種情況，必須先不要display:none，然後在jscrollpane套用以後，再將div做隱藏，教學如下

1.先找到function initialise()

2.接著在這個function的最後面加上$('#your div').hide()

意思就是，等所有初始化步驟結束以後，才把div的display設成none

其實有很多Jquery Plugin的套用，如果有用到顯示/隱藏的切換，都要注意到先後順序的問題

以上如有問題，歡迎一起討論