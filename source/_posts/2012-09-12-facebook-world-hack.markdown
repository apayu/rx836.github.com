---
layout: post
title: "[Facebook] Facebook Developer World HACK 2012"
date: 2012-09-12 23:42
comments: true
categories: 
---

因為本身的工作是開發Facebook相關社群APP，所以長期下來有在follow<a href="https://developers.facebook.com/blog/" target="_blank">Facebook Developer Blog</a>，看到<a href="https://developers.facebook.com/blog/post/2012/08/08/facebook-developer-world-hack-2012/" target="_blank">Facebook Developer World HACK 2012</a>原本以為應該跟以前一樣，只有幾個大城市才有舉辦，沒想到仔細一看，竟然有Taipei Taiwan！著實嚇了我一大跳，想當然爾是趕緊報名參加

<!--more-->

入場費蠻便宜的大概七百多塊，以下是我記錄的一些相片，因為是用手機拍的畫質不是很好多見諒

會場是位於信義區裡的克緹國際總部大樓，因為我是第一次參加這種HACK活動，所以我是事後才知道這大概是目前所有HACK活動場地最高級的一次，光看這個view就知道多棒

<img src="https://lh6.googleusercontent.com/-v_dRNzia9Lk/UFC9Tzbpx-I/AAAAAAAABe0/V-eKCYRGiNY/s788/IMG_2992.JPG" width="800px" />

整個會場都是落地窗玻璃，所以一整天參加活動甚至寫code都感到非常的舒服，尤其是下午的時候夕陽真的非常非常的漂亮

<img src="https://lh3.googleusercontent.com/-SchSdUumDww/UFDCG6u60OI/AAAAAAAABfc/oHuqMauFcQU/s788/IMG_2985.JPG" width="800px" />

這是在進去會場之前的報到，其實這是個類似天橋的地方，天橋旁有個空地可以看到整個信義區的view，我想跨年煙火在這看應該超HIGH的

<img src="https://lh5.googleusercontent.com/-PkjKD0yXXbw/UFC7Oui1G4I/AAAAAAAABeE/8cGsvgtZSP4/s788/IMG_2989.JPG" width="800px" />

進去後可以看到活動的大LOGO，是用中華民國的國旗所拼成的，可見Facebook多麼用心

<img src="https://lh6.googleusercontent.com/-nX29nNMaBBA/UFC7Qiw-HVI/AAAAAAAABeM/XDv-YGQnG1k/s788/IMG_2991.JPG" width="800px" />

當然還有領到一些東西，例如專屬徽章、T桖、還有貼紙，左邊那台是口譯機，Facebook相當貼心的請了同步翻譯人員，讓英文較不佳的人也可以知道講者在講什麼，而且是同步翻譯喔！

<img src="https://lh6.googleusercontent.com/-Xk3LqAjFKGg/UFC7iRksdEI/AAAAAAAABec/tX_5-Qu3fm8/s903/IMG_2994.JPG" width="800px" />

實體版的憤怒鳥XD，code寫累了可以來憤怒一下

<img src="https://lh6.googleusercontent.com/-Zb7ubBYygng/UFC7ZbaPDdI/AAAAAAAABeU/VdE3fIhCaTg/s788/IMG_2993.JPG" width="800px" />

吃不完的零食和喝不完的飲料是必備的，啤酒當然也是少不了

<img src="https://lh4.googleusercontent.com/-KdhIaeQwmZE/UFC9Prk4u8I/AAAAAAAABek/l-ZN1zb3XHc/s788/IMG_2998.JPG" width="800px" />

上午主要focus在Graph API部分，告訴大家怎麼利用Facebook做一些第三方的APP，也分享一些範例，但其實我蠻失望的，因為我原本會以為可以知道一些我從官方文件或Blog學不到的東西，不過後來想想也是，這本來就不是技術發表會，這是來推廣Facebook的Open Graph

<img src="https://lh3.googleusercontent.com/-u-licm0d5hg/UFC9XRWECvI/AAAAAAAABe8/Z7XsaVUYquE/s788/IMG_3003.JPG" />

然後Berlin也是跟我們台灣一樣11號舉行，但因為時差的關係我們進行到下午他們才正要開始，所以還有視訊同步Say Hello，還聽到有人開玩笑的大喊Hello World！ XDD

<img src="https://lh4.googleusercontent.com/-uz0E3PyUkgQ/UFC9R3twXkI/AAAAAAAABes/mWRevtEOLC4/s903/IMG_3001.JPG" />

因為下午時間就是開始寫code，但我大概接近中午的時候就開始寫了，因為我覺得我時間一定不夠，所以我一有想法就趕快開始動手了，順便簡單的分享一下我的心路歷程

第一次參加這種HACK活動，其實本來沒有什麼頭緒，甚至早上還都只是認為來這邊拜大神，吃喝一下就滿足了，可是後來在認識的前輩鼓勵之下，我也想來挑戰一下自己的極限，看看在這種氛圍底下我可以發揮到什麼程度，所以心一橫，我就決定來真的，好好拼一下

因為工作關係平常本來就是FB重度使用者，所以在發想要做啥這個階段，對我來說不是很困難，不過以後參加別的HACK就可能要先想好做什麼了，因為發想其實應該是最困難的，我想做的是因為我平常出去玩很喜歡用手機拍照上傳到FB，可是如果回家要寫BLOG的話，整理照片那些又很麻煩，所以我決定做一個簡單的工具，可以抓取妳出去玩的時候拍照上傳的照片，加上說明文字，並且幫你拼湊成HTML碼然後丟到HTML編輯器裡面，讓你按幾下就可以有一個BLOG的基本範本存在，而就不用煩惱BLOG要怎麼開頭

定好方向以後，就開始查官方文件，並且邊做邊調整細微的功能，因為是一人團隊的關係，所以我在ICON方面就用了bootstrap，省去了很多美工，Server端的code我也都沒寫，純粹都是用js來完成這個網站，結果一進入狀態以後，時間就過超快的，一下就天黑了

<img src="https://lh3.googleusercontent.com/-858tykFHwq0/UFC9XtZTnOI/AAAAAAAABfA/j-URBx8q624/s788/IMG_3005.JPG" width="800px" />

到了吃晚飯時間，我起來走了一下，發現還是很多人在拼呀


後來因為我沒注意到要上去DEMO的人要去網站註冊，所以我錯失了上台分享的機會，這讓我覺得蠻可惜的，雖然做的不是很好，但有一個展現自己的機會應該要好好把握

<img src="https://lh6.googleusercontent.com/-cJGtuvW_5ss/UFC9YhdCjcI/AAAAAAAABfE/dNz5OY_6rKo/s788/IMG_3007.JPG" width="800px" />

最後總共有30幾隊報名，大家真的都很厲害，而且評分有分好幾種得獎名額，例如最佳mobile或是最佳game，而且只要得獎都有IPAD可以拿，超大手筆的！不過只有第一名有機會去矽谷再跟全世界的人比一次

這是我人生的第一個HACK，真的收穫很多，也大開眼界，期許自己有一天能在上舞台分享我的東西，但在那之前可能要好好的加強自己的能力才行:)

