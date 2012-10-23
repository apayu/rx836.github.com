---
layout: post
title: "[Win8] 動態磚初體驗"
date: 2012-10-23 15:27
comments: true
categories: Win8
---

最近正參加<a href="http://www.microsoft.com/taiwan/promo/Win8AppFest/detailedRule.htm" target="_blank">Idea × Quality × Speed – Apps 開發者聯盟</a>，想爭取快手獎前100名名額，活動辦法中有提到需符合10項建議中的其中兩項(詳情看活動辦法)，我覺得動態磚是Win8 APP很有特色的一項功能，所以決定把他加入到我的APP，順便學習如何操作動態磚:)

<!--more-->

如果還不太了解Win8 APP的朋友，可以參考之前的<a href="http://blog.rx836.tw/blog/first-win8-app/" target="_blank">[Win8] 入門要學說Hello World</a>

在Win8 APP一開始可以從**資訊清單**裡面設定**預設磚**，預設磚會在應用程式第一次安裝時顯示

點擊package.appxmanifest兩下開啟資訊清單編輯器

<img src="https://lh5.googleusercontent.com/-op8a6QflCRY/UIZeWzVBBTI/AAAAAAAABt4/5HGif4Mh8hY/s813/A.png" />

**標誌:** 是正方形磚的圖檔設定

**寬標誌:** 是寬型磚的圖檔設定

**小標誌:** 是提供搜尋結果的小圖

<img src="https://lh3.googleusercontent.com/-PxTwOp3yqSo/UIZeXz4taNI/AAAAAAAABuA/_61SB2q6UtI/s518/B.png" />

上面的顯示圖1為方形磚，2為寬型磚

### 注意事項

這邊有一點要**特別特別注意**的是，對Win8 APP來說，假如沒有在資訊清單裡面設定**寬標誌**，應用程式將無法切換成寬型磚，所以寬型通知將也無法顯示，小弟我就是在這邊卡了很久，想說程式都沒有錯，為什麼一直無法顯示寬型通知...

假設你的應用程式有提供寬標誌，對應用程式按下右鍵，就會有選項可以選擇放大或縮小

<img src="https://lh3.googleusercontent.com/-1rzB4IyyrZI/UIZeYR6tFBI/AAAAAAAABuI/6aKtLu5S_pA/s570/C.png" />

OK，對動態磚有基本的認識以後，接下來就是JavaScript部份

先宣告一個notifications變數，這裡宣告的目的是取代完整的命名空間，省去每次都要打很長一串程式碼

	var notifications = Windows.UI.Notifications;
	
接下來就是為你的寬型磚挑選一個範本，並且抓取他的XML內容

	var template = notifications.TileTemplateType.tileWideImageAndText01;                      
	var tileXml = notifications.TileUpdateManager.getTemplateContent(template);
	
動態磚裡面的顯示內容其實就是一個XML的格式，所以我們利用**GetTemplateContent** 方法傳回 **XmlDocument**，也就是下列的XML基本架構

	<tile>
		<visual>
			<binding template="TileWideImageAndText01">
				<image id="1" src=""/>
				<text id="1"></text>
			</binding>
		</visual>
	</tile>
	
後續我們就是透過標準DOM函式來修改這個XML的內容，例如新增文字和新增圖片

新增文字

	var tileTextAttributes = tileXml.getElementsByTagName("text");   
	tileTextAttributes[0].appendChild(tileXml.createTextNode("我是寬型磚通知"));
	
新增圖片

	var tileImageAttributes = tileXml.getElementsByTagName("image");
	tileImageAttributes[0].setAttribute("src", "http://i.msdn.microsoft.com/dynimg/IC612768.png");
	tileImageAttributes[0].setAttribute("alt", "red graphic");	
	
以上設定完寬磚型通知以後，接下來是方形磚通知

	var squareTemplate = notifications.TileTemplateType.tileSquareText04;
	var squareTileXml = notifications.TileUpdateManager.getTemplateContent(squareTemplate);
	var squareTileTextAttributes = squareTileXml.getElementsByTagName("text");   
	squareTileTextAttributes[0].appendChild(squareTileXml.createTextNode("我是方型磚通知"));
	
然後將方型磚通知加到XML節點裡面

	
	var node = tileXml.importNode(squareTileXml.getElementsByTagName("binding").item(0), true);
	tileXml.getElementsByTagName("visual").item(0).appendChild(node);
	
最後就是利用XML來建立新的通知

	var tileNotification = new notifications.TileNotification(tileXml);

按下Ctrl+F5來看看效果吧

<img src="https://lh6.googleusercontent.com/-qKWHXg0ND0Y/UIZeZSVxekI/AAAAAAAABuQ/xU26ZDJgRIA/s771/D.png" />

<img src="https://lh3.googleusercontent.com/-1hIF3GPJNp4/UIZeZngTBII/AAAAAAAABuU/T3AO20DhkAI/s771/E.png" />

另外微軟建議通知的內容需要有時效性，所以建議磚的內容不應該超過通知訊息的時效性，也就是說太老舊的訊息就不要再通知囉~，記得幫通知加個時效性，以下程式碼是指10分鐘後將會把通知從磚移除

	var currentTime = new Date();
	tileNotification.expirationTime = new Date(currentTime.getTime() + 600 * 1000);

	notifications.TileUpdateManager.createTileUpdaterForApplication().update(tileNotification);

參考資料:

<a href="http://msdn.microsoft.com/zh-tw/library/windows/apps/hh465439.aspx" target="_blank">傳送磚更新 (使用 JavaScript 和 HTML 的 Metro 樣式應用程式)</a>

<a href="http://msdn.microsoft.com/zh-tw/library/windows/apps/hh779724.aspx" target="_blank">磚與磚通知概觀 (Metro 樣式應用程式)</a>

內容如有錯誤，歡迎指正