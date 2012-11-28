---
layout: post
title: "[jQ-Plugin] 有效降低會員註冊退信率的mailcheck"
date: 2012-11-28 12:04
comments: true
categories: jQ-Plugin
---

<img src="https://lh5.googleusercontent.com/-dLci9WLFC-8/ULWyqQJ-OxI/AAAAAAAAB_U/odHWaG3jNfE/s482/w.jpg" />

免費檔案分享<a href="http://kicksend.com/" target="_blank">Kicksend</a>有寫一篇文章是關於<a href="http://blog.kicksend.com/how-we-decreased-sign-up-confirmation-email-bounces-by-50/" target=_blank"">如何降低退信率</a>，內容大概是講User註冊會員以後，會發送註冊的確認信，但常常會發生被退信的情況，導致會員收不到信可能必須重新申請一次帳號，不然就是請客服修改E-mail，所以Kicksend為了減少這個困擾就做了分析並且解決問題

<!--more-->

Kicksend發現有很多人被退信的原因都是在輸入電子郵件(E-mail)的時候打錯domain，例如“hotmail.con”、“gnail.com”、“yajoo.com”等，這種錯誤有時候用戶自己都不知道，就直接按送出，導致收不到註冊信，所以Kicksend就做了一個設計，在用戶輸入E-mail以後，會檢查E-mail的domain，如果發現疑似錯誤情形，就會跳出建議的選項問用戶要不要更改，做到良好的 **user experience**，用了這個方法以後也確實降低了50%的退信率，無形中也增加了不少用戶，而下面將介紹這套jQuery plugin - **mailcheck**

##start

首先，可以去github載回原始碼

<a href="https://github.com/Kicksend/mailcheck" target="_blank">mailcheck</a>

接著在網頁裡面載入jQuery和mailcheck.min

	<script src="jquery.min.js"></script>
	<script src="mailcheck.min.js"></script>

html部分，一個text field

	<input id="email" name="email" type="text" />
	
接著是js部份

	var domains = ['hotmail.com', 'gmail.com', 'aol.com'];
	var topLevelDomains = ["com", "net", "org"];

	var superStringDistance = function(string1, string2) {
	  // a string distance algorithm of your choosing
	}

	$('#email').on('blur', function() {
	  $(this).mailcheck({
		domains: domains,                       // optional
		topLevelDomains: topLevelDomains,       // optional
		distanceFunction: superStringDistance,  // optional
		suggested: function(element, suggestion) {
		  // callback code
		},
		empty: function(element) {
		  // callback code
		}
	  });
	});

「domains」、「topLevelDomains」、「distanceFunction」這三個參數都是選填，分別為

**domains**: 要比對的domain，例如:yahoo.com、google.com

**topLevelDomains**: 允許的topLevelDomain，例如:com、net

**distanceFunction**: 自訂用來計算最接近topLevelDomain內容的函式

假設在沒有填寫 **domains** 和 **topLevelDomains** 情況下，會採用預設值，根據source code裡面所寫的預設值為

預設domains

	defaultDomains: ["yahoo.com", "google.com", "hotmail.com", "gmail.com", "me.com", "aol.com", "mac.com",
      "live.com", "comcast.net", "googlemail.com", "msn.com", "hotmail.co.uk", "yahoo.co.uk",
      "facebook.com", "verizon.net", "sbcglobal.net", "att.net", "gmx.com", "mail.com"]
	  
預設topLevelDomains

	defaultTopLevelDomains: ["co.uk", "com", "net", "org", "info", "edu", "gov", "mil"]

而「suggested」和「empty」則分別是 **輸入錯誤時的callback** 和 **沒填寫E-mail的callback**，所以你可以自行在這裡加上程式碼提醒User輸入錯誤或忘記輸入

###沒有jQuery的情況下

假如你的專案裡面沒有用到jQuery，也可以單純使用js版本

	Kicksend.mailcheck.run({
	  email: yourTextInput.value,
	  domains: domains,                       // optional
	  topLevelDomains: topLevelDomains,       // optional
	  distanceFunction: superStringDistance,  // optional
	  suggested: function(suggestion) {
		// callback code
	  },
	  empty: function() {
		// callback code
	  }
	});

最後附上有用到mailcheck這項效果的網站
<ul>
<li><a href="http://kicksend.com/" target="_blank">Kicksend</a></li>
<li><a href="http://dropbox.com/" target="_blank">Dropbox</a></li>
<li><a href="http://flotype.com/" target="_blank">Flotype</a></li>
<li><a href="http://kickstarter.com/" target="_blank">Kickstarter</a></li>
<li><a href="http://kippt.com/" target="_blank">Kippt</a></li>
<li><a href="http://minecraft.net/" target="_blank">Minecraft</a></li>
<li><a href="http://prispy.com/" target="_blank">Prispy</a></li>
<li><a href="http://sbnation.com/" target="_blank">SB Nation</a></li>
<li><a href="http://show-space.com/" target="_blank">Show Space</a></li>
<li><a href="http://theverge.com/" target="_blank">The Verge</a></li>
<li><a href="http://uber.com/" target="_blank">Uber</a></li>
</ul>

###參考資料:

<a href="https://github.com/Kicksend/mailcheck" target="_blank">mailcheck Github</a>

<a href="http://kicksend.com/join" target="_blank">Demo</a>

<a href="http://blog.kicksend.com/how-we-decreased-sign-up-confirmation-email-bounces-by-50/" target="_blank">How we decreased sign up confirmation email bounces by 50%</a>

內容如有錯誤，歡迎指正