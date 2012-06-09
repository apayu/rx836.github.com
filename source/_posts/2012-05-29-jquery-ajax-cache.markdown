---
layout: post
title: "[Jquery] AJAX cache讓IE一直抓到舊資料"
date: 2012-05-29 01:24
comments: true
categories: 
---
說真的魔鬼真的藏在細節裡面，很多我們不經意的忽略，都有可能在往後成為災難，我想這已經是幾乎每個開發者一定會經歷的事情，所以這一次，我就遇到災難了
<!--more-->

但好險的是，這次的災難又多虧了Google大神，幫我度過這次難關，事情是這樣的，我用Asp.net做了一個ashx的檔案，前端用Jquery的$.ajax()做AJAX的資料取得，目的是希望User每按一次按鈕就取得一筆新的資料

誰知道在Firefox和Chrome都正常，唯獨只有IE不管怎麼取都是舊的資料，後來看了<a href="http://blog.darkthread.net/" target="_blank">黑暗執行緒</a>的<a href="http://blog.darkthread.net/post-2009-06-03-about-jquery-ajax-cache-option.aspx" target="_blank">關於jQuery AJAX cache參數</a>我才知道，要在$.axaj()裡的參數cache設成false

	cache: false

這樣就不會再抓cache而讓資料怎麼抓都抓不到新的

另外還有這篇關於GET與POST的文章也很值得一讀!

<a href="http://blog.darkthread.net/blogs/darkthreadtw/archive/2009/04/16/dont-use-get-ajax.aspx">隱含殺機的GET式AJAX資料更新</a>


以上如有錯誤或疑問，歡迎一起討論喔!