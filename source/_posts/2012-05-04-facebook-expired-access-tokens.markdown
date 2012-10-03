---
layout: post
title: "[Facebook]關於FB access tokens過期的處理"
date: 2012-05-04 22:45
comments: true
categories: Facebook
---
Facebook已經在5/1號移除offline_access的權限，也就是說之後將不再支援offline_access，小弟我英文不是很好，官方文件沒辦法翻譯完全，但我會將我的解法跟大家分享
<!--more-->

如果你的Facebook APP都是User在應用程式裡面**立即**完成動作的話，幾乎不用考慮access tokens時效性的問題，但如果你有一些不是當下立刻執行，而是可能過多久以後才執行動作，例如:**幾小時後發一篇訊息到塗鴉牆**，或是像我一樣，寫了一隻app可以**預約上傳照片的APP**，就有可能面臨到access tokens過期問題

依照Facebook他們的文件所寫，access tokens過期總共會有四種情況

###1.The token expires after expires time (2 hours is the default)###

因為太久沒更新access tokens而導致過期(預設是1-2小時之間)

###2.The user changes her password which invalidates the access token###

User改變登入時的密碼

###3.The user de-authorizes your app###

User移除掉你的APP驗證(在帳號設定->應用程式)

###4.The user logs out of Facebook.###

User登出Facebook

以上四種情況都會導致時效過期，但在新的整合之下，雖然預設只有1-2個小時的時效，但實際上可透過延長來達到60天的期限

首先用Javascript SDK用一般取得access tokens的方法

	FB.getLoginStatus(function(response) {
            if (response.authResponse) {
                //FB User ID
                var u_fbid = response.authResponse.userID;                
                //FB accessToken
                var access_token = response.authResponse.accessToken;                
            } else {
                login();
                // no user session available, someone you dont know
            }
        });

取得壽命較短的access tokens(short-lived)以後，再透過GET取得較長的access tokens(long-lived)，已擴展到60天的時效，這裡我用Jquery的$.ajax來取得

	save_u = [
                            { name: "client_id", value: APP_ID },
                            { name: "client_secret", value: APP_SECRET },
                            { name: "grant_type", value: 'fb_exchange_token' },
                            { name: "fb_exchange_token", value: EXISTING_ACCESS_TOKEN  }
                       ];
                $.ajax({
                    type: "GET",
                    url: "https://graph.facebook.com/oauth/access_token",
                    data: save_u,
                    success: function(data) {
                        console.log(data);
                        });
                    }
                });

APP_ID和APP_SECRET從你設定APP的地方就可以看到，grant_type的值照抄就是fb_exchange_token，而參數fb_exchange_token要給的值就是你剛所取得較短的access tokens

接著Facebook就會回傳一串值回來

	access_token=xxxxxxxxxxxxxxxxx&expires=5183914
	
xxx那些就代表著新的並且擁有60天期限的access tokens

而期限5183914就是秒數，算一算剛好差不多是60天的時間沒錯


雖然目前使用都是OK，但如果我有新的心得還是會再上來與大家分享，那如果文章裡有錯誤的話，也請不吝於指正，另外參考連結裡面有PHP的範例可以作為參考

參考:

<a href="https://developers.facebook.com/blog/post/2011/05/13/how-to--handle-expired-access-tokens/">How-To: Handle expired access tokens</a>

<a href="https://developers.facebook.com/roadmap/offline-access-removal/">Removal of offline_access permission</a>
	
	
