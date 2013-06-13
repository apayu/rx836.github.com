---
layout: post
title: "[jQ-Plugin] 如何減少User密碼輸入錯誤?"
date: 2013-06-13 18:35
comments: true
categories: jQ-Plugin
---

<img src="http://farm8.staticflickr.com/7394/9032388794_c9ce2d4e25_o.jpg" />

"Becaues life's too short waste time re-typing passwords"

生命短暫，別浪費時間重新輸入你的密碼

<!--more-->

在製作登入頁面時，常會使用到 &lt;input  type="password" &gt; 這個輸入密碼的 HTML 控制項，預
設的情況下，當你在密碼輸入框輸入密碼時，都會出現‧‧‧這樣的小黑點

好處是可以防止旁人知道你輸入的密碼是什麼，但好意有時候會讓人覺得不方便，尤其這個狀況發生在
移動裝置時

怎麼說呢？原因出在於移動裝置設備通常因為螢幕尺寸大小的關係，鍵盤通常不好點擊，以 IPHONE 為
例，當我想點 G 的時候，可能因為我的手指肥大，而點到旁邊的H，雖然每次點擊時，輸入框上面會秀
出當下所按的字母，但總是有時候會忽略的時候，如果突然手一個不順，自己到底有沒有輸入正確，恐
怕很難曉得，所以如果能讓使用者選擇切換，是否可以看的到密碼，或許是個不錯的使用者體驗

##Start

詳細的範例可以從 github

<a href="https://github.com/cloudfour/hideShowPassword#hideshow-password-plugin-for-jqueryzepto" target="_balnk">Download</a>

這裡做個簡單的範例

HTML部份

	<figure>
	  <div class="login">
		<input type="text" placeholder="Username" >
		<input id="password-1" type="password" placeholder="Password">
	  </div>
	  <figcaption>Inner toggle styled as icon.</figcaption>
	</figure>

CSS部份

	.hideShowPassword-toggle {
		background-image: url(img/wink.svg);
		background-position: 0 center;
		background-repeat: no-repeat;
		cursor: pointer;
		height: 100%;
		overflow: hidden;
		text-indent: -9999em;
		width: 44px;
	}

這裡最主要是幫切換的按鈕做修飾，如同github裡面的範例一樣加上圖片

js部份

	<script type="text/javascript" src="vendor/jquery.js"></script>	
	<script src="hideShowPassword.min.js"></script>
	<script>
		// Example 1
		$('#password-1').hideShowPassword({
		  // Creates a wrapper and toggle element with minimal styles.
		  innerToggle: true
		});
	</script>

以上是簡單的實做範例，會出現一個眼睛讓你做切換是否顯示密碼

<img src="http://farm6.staticflickr.com/5451/9032954004_208664f24e_o.jpg" />

還有其他 methods 可以應用

	$('#password').showPassword(); // Reveal
	$('#password').hidePassword(); // Hide
	$('#password').togglePassword(); // Toggle

或是

	$('#password').hideShowPassword(true); // Reveal
	$('#password').hideShowPassword(false); // Hide
	$('#password').hideShowPassword('toggle'); // Toggle

利用這些可以自己用 checkbox 來切換，做出一樣的效果

這裡有 <a href="http://cloudfour.github.io/hideShowPassword/" target="_blank">完整的範例</a> 可以看
	
##參考資料:

<a href="http://blog.cloudfour.com/hide-show-passwords-plugin/" target="_blank">Hide/Show Passwords: The Missing Plugin</a>

<a href="http://www.lukew.com/ff/entry.asp?1653" target="_blank">Mobile Design Details: Hide/Show Passwords</a>

內容如有錯誤，歡迎指正