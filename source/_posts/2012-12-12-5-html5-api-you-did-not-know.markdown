---
layout: post
title: "[HTML5] 5個你可能不知道的HTML5 API"
date: 2012-12-12 06:46
comments: true
categories: HTML5
---

HTML5已經火紅了一陣子，姑且不論他到底能不能主宰未來的網頁技術，達到一統江山，天下太平(?)的目的，至少現在已經越來越多人開始將HTML5應用在實際的專案上，小弟雖然目前還沒大量使用到新技術，但今天還是來分享五個可能比較少人知道的，HTML和JavaScript API，希望讓大家多了解HTML5還有哪些新玩意

<!--more-->

##Fullscreen API

最近或許在網路上看過一些可以做全螢幕效果的jQuery plugin，實現這個效果用到的就是 **Fullscreen API**，範例如下

	function launchFullScreen(element) {
	  if(element.requestFullScreen) {
		element.requestFullScreen();
	  } else if(element.mozRequestFullScreen) {
		element.mozRequestFullScreen();
	  } else if(element.webkitRequestFullScreen) {
		element.webkitRequestFullScreen();
	  }
	}
	
	launchFullScreen(document.documentElement); // the whole page
	launchFullScreen(document.getElementById("videoElement")); // any individual element

你可以給予整個HTML做整頁的全螢幕，也可以單獨給某個ID的元素，但有一點要注意的是，我在寫範例時需加上一些動作去 **啟動** 全螢幕，例如點擊某個button之類的，而不能在一進入頁面就啟用全螢幕模式，這點跟 **另開啟視窗** 有點像，另外在啟用前瀏覽器會詢問你是否允許全螢幕，如下圖

<img src="https://lh6.googleusercontent.com/--HepWolPOjY/UMe36hSpsNI/AAAAAAAACEA/mMSMIKo40F8/s692/aaa.jpg" />

這效果經常用在一些遊戲上面，例如擁有第一人稱視角的射擊遊戲 - <a href="https://developer.mozilla.org/en-US/demos/detail/bananabread" target="_blank">BananaBread</a>

##Page Visibility API

<img src="https://lh4.googleusercontent.com/-IDcX0ql8dOs/UMe36kP6YKI/AAAAAAAACD8/Jg5gmM5w4OI/s370/a2.jpg" />

老實說第一次Demo這個API的效果覺得還蠻好笑的...，就如同範例一樣，他可以讓開發者監控User是不是在此頁籤，可以從範例效果得知，當我離開此頁籤時，HTML Title就會改成 "我又跳出去了"，如果回到此頁籤當中，就會改回 "我又跳進來了"，其實還蠻欠打的...，阿不是，是蠻實用的XD

	// Adapted slightly from Sam Dutton
	// Set name of hidden property and visibility change event
	// since some browsers only offer vendor-prefixed support
	var hidden, state, visibilityChange; 
	if (typeof document.hidden !== "undefined") {
	  hidden = "hidden";
	  visibilityChange = "visibilitychange";
	  state = "visibilityState";
	} else if (typeof document.mozHidden !== "undefined") {
	  hidden = "mozHidden";
	  visibilityChange = "mozvisibilitychange";
	  state = "mozVisibilityState";
	} else if (typeof document.msHidden !== "undefined") {
	  hidden = "msHidden";
	  visibilityChange = "msvisibilitychange";
	  state = "msVisibilityState";
	} else if (typeof document.webkitHidden !== "undefined") {
	  hidden = "webkitHidden";
	  visibilityChange = "webkitvisibilitychange";
	  state = "webkitVisibilityState";
	}

	// Add a listener that constantly changes the title
	document.addEventListener(visibilityChange, function() {
	  if(document[state]=='visible'){
		document.title = '我又跳進來了';
	  }else if(document[state]=='hidden'){
		document.title = '我又跳出去了';
	  }
	}, false);

	// Set the initial value
	document.title = '我又跳進來了';
	
##getUserMedia API

這個API很酷的地方在於可以利用一些電腦的視訊媒體做互動!例如像是操作筆電的webcam，搭配&lt;canvas&gt;可以做到拍攝照片的效果

	// Put event listeners into place
	window.addEventListener("DOMContentLoaded", function() {
	  // Grab elements, create settings, etc.
	  var canvas = document.getElementById("canvas"),
		context = canvas.getContext("2d"),
		video = document.getElementById("video"),
		videoObj = { "video": true },
		errBack = function(error) {
		  console.log("Video capture error: ", error.code); 
		};

	  // Put video listeners into place
	  if(navigator.getUserMedia) { // Standard
		navigator.getUserMedia(videoObj, function(stream) {
		  video.src = stream;
		  video.play();
		}, errBack);
	  } else if(navigator.webkitGetUserMedia) { // WebKit-prefixed
		navigator.webkitGetUserMedia(videoObj, function(stream){
		  video.src = window.webkitURL.createObjectURL(stream);
		  video.play();
		}, errBack);
	  }
	}, false);
	
可以直接看很強大的 <a href="http://davidwalsh.name/demo/camera.php" target="_blank">Demo</a> 部份(記得使用Google Chrome效果較佳)

##Battery API

我想這個應該不難理解，可以直接取得你目前設備的電池使用狀況，雖然目前還不普及，但至少已經證明了未來用HTML5技術是有可能對硬體底層做操作:)

	// Get the battery!
	var battery = navigator.battery || navigator.webkitBattery || navigator.mozBattery;

	// A few useful battery properties
	console.warn("Battery charging: ", battery.charging); // true
	console.warn("Battery level: ", battery.level); // 0.58
	console.warn("Battery discharging time: ", battery.dischargingTime);

	// Add a few event listeners
	battery.addEventListener("chargingchange", function(e) {
	  console.warn("Battery charge change: ", battery.charging);
	}, false);

一樣可以直接看 <a href="http://davidwalsh.name/demo/battery-api.php" target="_blank">Demo</a>，我用筆電開啟Firefox測試果然還蠻準的，真的就是98%

<img src="https://lh4.googleusercontent.com/-ZCusQMl_zlw/UMe36s4-QnI/AAAAAAAACEE/Rih2Tvfj3os/s323/a3.jpg" />

##Link Prefetching

這個API特別的地方在於，假如你先在HTML裡面加上下面這些Tag，瀏覽器就會在背後偷偷的預先載入這些資源，讓你在連結這些link的時候可以有更順暢的體驗


	<!-- full page -->
	<link rel="prefetch" href="http://davidwalsh.name/css-enhancements-user-experience" />

	<!-- just an image -->
	<link rel="prefetch" href="http://davidwalsh.name/wp-content/themes/walshbook3/images/sprite.png" />
	
以上五個是比較少見的HTML5 API，有些雖然瀏覽器的支援普及度不高，但整體來說都是對User好的使用者體驗，提早先熟悉對開發者來說是件好事，希望以後可以真的大量運用在Web應用程式當中
	
###參考資料:

<a href="http://davidwalsh.name/more-html5-apis" target="_blank">5 More HTML5 APIs You Didn’t Know Existed</a>

內容如有錯誤，歡迎指正