---
layout: post
title: "[Facebook] 如何建立facebook App 且取得FB ID"
date: 2012-06-16 00:36
comments: true
categories: 
---

這裡將會紀錄如何建立一個Facebook App，並且讓User授權應用程式，最後取得FB ID來當會員資料或是參加活動的ID識別

<!--more-->

首先，你必須是個Facebook App Developers，你可以去<a href="https://developers.facebook.com/" target="_blank">facebook DEVELOPER</a>申請你的身份，我記得以前不用手機驗證，但現在則需要

接著你會看到以下畫面

<img src="https://lh3.googleusercontent.com/-qsrR5jf8ieQ/T9tcfJx0g0I/AAAAAAAAAQo/ijDj_DOzoFY/s902/2012-06-15_170640.jpg" width="700px" />

點選右上角的Create New App

會跳出一個POP視窗

<img src="https://lh4.googleusercontent.com/-b1KPFkV9kak/T9tdnIs-8LI/AAAAAAAAAQ4/Qa62h_PbpYw/s660/2012-06-15_171009.jpg" width="700px" />

**App Name**:指的是你的應用程式名稱

**App Namespace**:是你的網址命名

**Web Hosting**:如果你有自己的Web Hosting就不用勾選

按下Continue以後會出現填寫驗證碼，填寫完後按下Submit

<img src="https://lh6.googleusercontent.com/--MZXrFzYUmo/T9tdnPmoYLI/AAAAAAAAAQw/tjvCiZFjhaU/s664/2012-06-15_171639.jpg" width="700px" />

然後就會看到建立好的App一些資訊和設定

<img src="https://lh3.googleusercontent.com/-HmL8gmkIbMo/T9tdnPYDjgI/AAAAAAAAAQ0/aoxRueaQ4uQ/s882/2012-06-15_171904.jpg" width="700px" />

因為雖然是寫Facebook App，但其實Facebook只是提供你API和外框包住你的網頁，所以你還要提供你的網頁所在位置給Facebook

<img src="https://lh6.googleusercontent.com/-WAH8_0uqxXY/T9tdnoOUwDI/AAAAAAAAAQ8/Ol4WZwkLFI8/s729/2012-06-15_172431.jpg" width="700px" />

要注意的是Facebook要求<a href="https://developers.facebook.com/blog/post/497/" target="_blank">使用加密的https</a>，所以如果你如果沒有的話，可能要花錢購買這方面的憑證

到這邊為止，已經建立好初步的Facebook App了


##使用JavaScript API做授權##

有了App以後，我們要跟網頁串起來，因為我是.NET開發者，所以我會先建立一個index.aspx，接著一般我都會在&lt;form id="form1" runat="server"&gt;&lt;/form&gt;的後面加上

	<div id="fb-root"></div>
	<script type="text/javascript" src="https://connect.facebook.net/zh_TW/all.js"></script>  
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js" type="text/javascript"></script>
    	
 注意，如果沒有fb-root的div會導致不能使用Facebook API，另外我還多用了Jquery來方便等一下寫js程式碼
 
接下來新增一個div做為點選授權
 
 	<div id="btn">點我授權</div>

接著是js初始化部分

	$(function () {
	
            var _app_id = 'Your App ID';
            var _api_key = '';
            //驗證            
            FB.init({
                appId: _app_id,
                status: true, // check login status
                cookie: true, // enable cookies to allow the server to access the session
                xfbml: true, // parse XFBML                
                oauth: true // enable OAuth 2.0
            });
            FB.Canvas.setAutoGrow(); //autoResize  → no scrollbar
            
       });

**Your App ID**必須填入你建立好的Facebook App裡面的App ID ，接著加上點擊觸發授權的js部分

		$('#btn').click(function () {
                getLoaginState();
            });

            //驗證
            function getLoaginState() {
                FB.getLoginStatus(function (response) {
                    if (response.authResponse) {
                        var u_fb_id = response.authResponse.userID;
                        console.log(u_fb_id);
                    } else {
                        login();                        
                    }
                });
            }

            //跳出登入視窗
            function login() {
                FB.login(function (response) {
                    if (response.authResponse) {
                         var u_fb_id = response.authResponse.userID;
                         console.log(u_fb_id);
                    } else {
                        alert('須同意應用程式');
                    }
                });
            }
 
這段js是綁定一個click事件，在id為btn的div上，然後去執行getLoaginState()，**FB.getLoginStatus**是看登入狀態，沒有登入則會跳到login()，console是等下能看到我們所取得的FB ID


接著在剛剛App設定網址那邊有個**Canvas Page**，那就是你掛在Facebook底下的網址，後面的網址名稱就是你剛剛設定的App Namespace，進入以後會看到以下畫面

<img src="https://lh3.googleusercontent.com/-j1YbMlBI6oU/T9tgEdDILSI/AAAAAAAAARY/noBT1wLBEEs/s1223/2012-06-16_001702.jpg" width="700px" />

按下**點我授權**，就會跳出授權是否同意應用程式視窗


<img src="https://lh5.googleusercontent.com/-ul15BASQCTk/T9th2pskfsI/AAAAAAAAARg/E9_uWLPQVFI/s1046/2012-06-16_002409.jpg" width="700px" />

同意以後，就可以在firebug裡面看到我們剛剛所加的console，秀出你的FB ID

<img src="https://lh5.googleusercontent.com/-ITJVUoACd3s/T9tirDBGMOI/AAAAAAAAARo/Oy8ICJf03bw/s1008/2012-06-16_002811.jpg" width="700px" />

得到FB ID可以利用<a href="https://developers.facebook.com/docs/reference/api/" target="_blank">Graph API</a>再更進一步取得許多資料，當然也要先授權相關權限才行

以上如有問題，歡迎一起討論