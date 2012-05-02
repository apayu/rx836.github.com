---
layout: post
title: "如何開啟 Disqus與和常見的指令"
date: 2012-04-27 02:12
comments: true
categories: 
---

經營Blog不是一件簡單的事情，尤其是還是自己架Blog的情況下，更是挫折連連，真的是憑藉著一股不知哪來的傻勁，遇到問題就找找資料，土法煉鋼好像也能做出一把堪用的武器出來
<!-- more  -->
## 為什麼我沒有Comments..
對呀...，為什麼我沒有Comments，沒想到第一個遇到的問題就是這麼看似平凡，但對於我這個新手來說，卻是不知如何是好的難題，好險網路上還是有很多人願意紀錄這一切

<a href="http://gangmax.github.com/blog/2012/01/20/how-to-use-disqus-in-octopress/" target="_blank">Blog of GangMax : How to Use Disqus in Octopress</a>

簡單來說就是需先申請<a href="www.disqus.com/" target="_blank">disqus</a>帳號，接著將你的disqus_short_name填在**_config.yml**裡面

	disqus_short_name: your_disqus_short_name
	disqus_show_comment_count: true

## 一些常用的指令

說來可憐...，我到現在還不會在不同台電腦編寫我的Octopress，最近嘗試一次結果因為不熟git而把檔案搞得亂七八糟，但最近有找到一篇文章，我是還沒有親自嘗試過，但想要在這邊先記錄下來，以方便我回頭來看

<a href="http://shanewfx.github.com/blog/2012/02/16/clone-blog-from-github/" target="_blankl">思考的轨迹 : 如何维护Github上博客</a>

然後常用的指令有

**設置Octopress與Github做連結**

	rake setup_github_pages
**新增文章**

	rake new_post["title"]
**產生_deploy，也就是將你source裡面的檔案轉換成html放到_deploy**

	rake generate
**發佈_deploy到Github上**

	rake deploy
**假使用UTF-8編碼，必須先設定這兩行**	

	set LC_ALL=zh_TW.UTF-8
	set LANG=zh_TW.UTF-8
**將Octopress原始碼放到Github分支Source上(Master是放_deploy)**	

	git add .
	git commit -m "your message"
	git push origin source	
	
這還真是一篇＂筆記＂的文章...	
	