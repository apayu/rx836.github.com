---
layout: post
title: "[jQ-Plugin] 用jQuery打造alert、confirm和prompt dialogs"
date: 2013-01-24 11:21
comments: true
categories: jQ-Plugin
---

<img src="https://lh3.googleusercontent.com/-Zmc0Ts3xud4/UQDnKqQMtiI/AAAAAAAACPg/x2E0ljNmpOM/s387/2013-01-24_115500.jpg" />

知名的網路趨勢觀察 Inside 有一篇文章 <a href="http://www.inside.com.tw/2013/01/23/app-dialog-button-design-should-yes-be-right-or-left" target="_blank">App 的 「確定」按鈕應該放在左邊還是右邊？</a>，裡面寫到關於使用者設計，iOS與 Android 的不同，我對這方面不是研究者，所以就不針對文章內容做討論，但同樣的事情回到 Web 部分，如果能將我們常看到的 alert 視窗做客製化，引導 User 做點擊，或許可以減少使用者誤按的情形發生

<!--more-->

##原生的彈跳視窗

一般我們常見的內建 confirm 和 alert，因為是原生的視窗元素，有時候難免會跟網站整體的視覺設計很不搭嘎，按鈕文字也無法修改，跟使用者間的互動就不是那麼的直覺，例如下面的範例圖

<img src="https://lh6.googleusercontent.com/-iYqFTOzua-4/UQDnKscNRXI/AAAAAAAACPc/lRsW6cDln3Q/s389/2013-01-24_121937.jpg" />

在填寫完表單以後，跳出了一個提醒視窗告知『獎品將在三天後寄出』，但當你按下『確定』時，心中難免會覺得**要確定的是甚麼**？但如果像下面這張圖一樣，做客製化文字

<img src="https://lh6.googleusercontent.com/-ygbraRujwkg/UQDnKjkwBnI/AAAAAAAACPk/mggASJ-uJxM/s582/2013-01-24_122158.jpg" />

User在使用時就不會有那些疑惑存在，整個視窗還可以搭配網站做設計，至於要怎麼客製化呢？下面是我的使用筆記

##Start

這裡我使用的是 Alertify 這款jQuery plugin ，可以到 github 下載source code

<a href="https://github.com/fabien-d/alertify.js/" target="_blank">DOWNLOAD SOURCE</a>

接著在 lib 資料夾裡面有兩個檔案，分別是 alertify.js 和 alertify.min.js，因為我們要做範例，所以使用方便 Debug 的 alertify.js

	<script type="text/javascript" src="http://code.jquery.com/jquery-1.8.2.js"></script>
	<script type="text/javascript" src="lib/alertify.js"></script>
	
接著是css部份

	<link rel="stylesheet" href="themes/alertify.core.css" />	
	<link rel="stylesheet" href="themes/alertify.default.css" />
	
如果要符合自己網站的設計，就修改 alertify.default.css 這支檔案即可

最後是js部份

	alertify.alert("獎品將在三天後寄出");
	
結果圖

<img src="https://lh6.googleusercontent.com/-NhnuNSV7ipE/UQDnLpYsIlI/AAAAAAAACPo/ZmiAC0GeGAA/s582/2013-01-24_153113.jpg" />

如果要修改文字的話，在前面加上 alertify.set() 的設定

	alertify.set({ labels : { ok: "了解", cancel: "取消" } });
	alertify.alert("獎品將在三天後寄出");
	
要做 confirm 視窗的話

	alertify.confirm("確定儲存嗎?", function (e) {
		if (e) {
			// user clicked "ok"
		} else {
			// user clicked "cancel"
		}
	});
	
結果圖

<img src="https://lh3.googleusercontent.com/-pQSeUPBhHZs/UQDnLnRK3yI/AAAAAAAACPs/mR20IrnuxJ4/s589/2013-01-24_153412.jpg" />

比較特別是還可以設置notifications

	alertify.success("Success notification");
	
在瀏覽器視窗的右下角就會出現notifications，並且會在幾秒後自動消失

<img src="https://lh3.googleusercontent.com/-x42wvO7nDIg/UQDnL_RqoFI/AAAAAAAACPw/N26mQw_xs5w/s607/2013-01-24_153713.jpg" />

##結論

這支 plugin 在使用上相當容易，而且還會在按鈕上加上光暈，引導使用者按下按鈕，樣式不喜歡的話，直接修改css檔案即可，有興趣的朋友可以下載回來試試

##參考資料:

<a href="http://fabien-d.github.com/alertify.js/" target="_blank">alertify.js</a>

內容如有錯誤，歡迎指正
