---
layout: post
title: "[Octopress]如何設定自己的Domain與異地編輯設定"
date: 2012-05-20 01:35
comments: true
categories: Octopress
---

用了將近一個月的Octopress，才慢慢覺得開始步上軌道，好笑的是我竟然誤以為因為Domain沒有設定，才會導致Google搜尋不到我的文章...，更慘的是，匆忙的利用網銀買了一組自己的Domain回來後，才發現原來我淺到連DNS都不會設定...
<!--more-->

能把這麼丟臉的事情都昭告天下，就是我認為人就是要認清自己，不會的東西就是要主動去尋求答案，不懂的事情也不要怕丟臉被別人知道，因為我深信，不可能每個人一出生就什麼事情都會，但唯有不肯面對自己的人....ㄟ!話題偏了


如果你要設定自己的一組Domain，首先必須先去買一組屬於自己的網址，像我因為之前有幫公司在PC HOME買過網址的經驗，所以我就直接挑選PC HOME做為買網址的服務

<a href="http://myname.pchome.com.tw/" target="_blank">PC HOME買網址</a>


買了網址等到他通知你服務開通，接著就是進去他的管理介面做設定，因為一般來說**DNS的設定大約要24小時**才能好，所以我會先建議這一步先做，但這裡就有血淚史可以講了...因為我不知道我自己的DNS設定的正不正確，所以都要等上一天，抱著滿懷期待的心情輸入網址，看見那404的畫面..，然後再重新設定一次DNS...，等24小時...，再一次的循環...

###好險國父革命11次，我只革命了七天，算是不幸中的大幸###

回到設定網址，參照官網是要使用**CNAME**的方式來設定網址，參照PC HOME 的說明是指CNAME，意思就是**別名 Aliases**，白話的意思就是將你的網域名稱對應到某個網站，所以我DNS的管理設定如下

	主機 / 次網域 | 地址 | 類型
	blog |  rx836.github.com. | CNAME
	
接著就是Octopress的設定，一樣在指令模式下輸入

	echo 'your-domain.com' >> source/CNAME
	
**your-domain.com**就是你的Domain，例如我的是blog.rx836.tw

然後妳就會在source看到多了一個名叫CNAME的檔案，用記事本打開還會看到你的Domain已經寫在裡面了，再來就是輸入

	rake generate
	
接著發佈

	rake deploy
	
然後好好睡一覺，等明天打開網址大喊

###爽啦!我終於設定好了###

可是設定好後，我還是在Google搜尋不到我的文章，Google Analytics怎麼看都只有我自己的流量，不奢求成為受歡迎的Blog客，但沒人可以一起分享總是覺得孤單，唱獨角戲的感覺很不真實，也就不會有寫文章的動力

所以我打算主動出擊，直接跑去別人的blog問(<a href="http://zespia.tw" target="_blank">http://zespia.tw/</a>)，果然社群都是很親切大方的，直接告訴我把**sitemap.xml**檔案這個丟到Google上就可以了!

<a href="https://www.google.com/webmasters/tools/" target="_blank">Google 網站管理工具</a>

利用網站管理工具先新增一個網站，接著提交sitemap就完成了，一段時間以後，你的網站就曝光在網際網路的茫茫大海之中，但排名或是SEO優化這部分就要看個人造化了

當你開始經營一個Blog時，你一定不會只想在一個地方撰寫Blog，有時候突如其來的想法或是問題分享，會讓你想要立刻打開編輯器做編輯，但Octopress不是一般的Blog，他需要先在本機做產生，再發佈，不像其他的Blog有個後台管理，所以異地編輯就需要花一些功夫

###這裡我是用Octopress+Github當教學###

首先你要有一台已經安裝好Octopress和Github(<a href="http://blog.rx836.tw/blog/first-octopress/" target="_blank">這裡教學</a>)的環境，接著Clone你的Blog到你新的這台電腦裡面

	git clone git@github.com:rx836/rx836.github.com.git
	
上面是我Github的SSH，你要換成自己的才行

接著要checkout出source

	cd rx836.github.com
	git checkout source
	
然後再重新設置github的設定做連結

	rake setup_github_pages

出現提示以後再輸入你的SSH

	git@github.com:rx836/rx836.github.com.git
	
接著在更新你的source

	git pull origin source
	
最後就可以看是要新增文章，還是編輯，產生，發佈，躺著，趴著，跪著，隨便怎麼做都可以了

一樣，在發佈Blog以後，別問了記得更新source到你的Github上，這樣另外一台才可以有最新的source可以用喔

	git add .
	git commit m 'mycommit'
	git push origin source
	
參考:<a href="http://shanewfx.github.com/blog/2012/02/16/clone-blog-from-github/" target="_blank">http://shanewfx.github.com/blog/2012/02/16/clone-blog-from-github/</a>	

以上教學分享，如有疑問或錯誤，歡迎一起討論