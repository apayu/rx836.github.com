---
layout: post
title: "[學習筆記] 免費玩Amazon Web Service(AWS) EC2"
date: 2012-10-30 11:25
comments: true
categories: 學習筆記
---

Amazon Web Service(AWS)從2006年開始就提供一些雲端服務，但我也是直到近期才開始真正的使用雲端帶來的方便，使用方式說起來也蠻簡單的，不過其實有很多細節與設定還要再多摸索，這次就先筆記怎麼開始使用AWS的EC2服務

<!--more-->

先來簡單介紹一下什麼是EC2(Elastic ComputeCloud，彈性雲端運算)，其實他就是一台虛擬主機，只要你會架站技術，就可以用遠端連線的方式，選擇安裝Linux或Windows Server 2008，不想使用的話也可以在後台直接關機或刪除虛擬主機，而且AWS最讓人著迷的就是使用多少才算多少錢，如果這個月服務想停止，那這個月就不會跟你算錢！這麼好的服務要怎麼申請呢？直接來看下面步驟

首先到<a href="http://aws.amazon.com/" target="_blank">AWS</a>首頁，選擇Sign up now

<img src="https://lh4.googleusercontent.com/-xqNCJQspknM/UI-FGSVVMGI/AAAAAAAABxo/HnD7qU0Zmvc/s1038/2012-10-30_114058.jpg" />

假如沒有Amazon的帳號，必須選擇 ** I am a new user** ，然後進行申請的步驟，如果已經擁有帳號，就直接選擇 **I am a returning userand my password is** ，並且輸入密碼，注意要使用AWS的服務必須要有信用卡，因為當你超過免費的使用上限才能直接收錢(無誤)

<img src="https://lh5.googleusercontent.com/-HyaQ3OppxQQ/UI-FGY4NJXI/AAAAAAAABxs/RWZ0aOeO_AQ/s915/2012-10-30_113758.jpg" />

申請帳號的過程都是填一些基本資料，和進行一些驗證，過程中就不多加說明了

OK，進來以後你就會看到這個畫面

<img src="https://lh3.googleusercontent.com/-HewOX42mZ4k/UI-FHoeHdXI/AAAAAAAABx4/3jnReVoz0ZM/s916/2012-10-30_115202.jpg" />

恩...琳瑯滿目的英文選項，但沒關係，我們只要挑選我們要的去了解，選擇左邊的 **AWS Management Console**

<img src="https://lh6.googleusercontent.com/-xDKUaMI1kp0/UI-FLs8jlSI/AAAAAAAAByE/hONoGXerkO0/s885/2012-10-30_115611.jpg" />

接著按下 **Sign in to the AWS Console**

<img src="https://lh3.googleusercontent.com/-ePuWgaQtyIs/UI-FL3IykXI/AAAAAAAAByM/Unm4rUDg308/s938/2012-10-30_115843.jpg" />

挑選 **EC2**

<img src="https://lh5.googleusercontent.com/-VlYPIrLzYgk/UI-FLlQrk7I/AAAAAAAAByA/Dhh-5voV3d0/s1137/2012-10-30_120015.jpg" />

這裡要注意的一點是，右上角在名稱的右邊，可以選擇主機的所在位置，鄉民是推薦日本，但如果你想架在別的地方也可以

<img src="https://lh3.googleusercontent.com/-L4HVl_bkCg0/UI-F7rDExDI/AAAAAAAAB0g/0Wi1AEjKEas/s344/2012-10-30_154605.jpg" />

接著點選 **Launch Instance**

<img src="https://lh5.googleusercontent.com/-F0dPwprEHwk/UI-FP_x-OvI/AAAAAAAAByY/9kTJDlGQ_jk/s1223/2012-10-30_144418.jpg" />

選擇 **Classic Wizard**，接著按下 **Continue**

<img src="https://lh5.googleusercontent.com/-k0dIMHJwYMc/UI-FQ320qmI/AAAAAAAAByg/sLJFd9FLEl0/s1223/2012-10-30_144558.jpg" />

如果要用free的話，記得要挑選 **Root Device Size** 在10G以內的服務，這裡我們選擇的是 **Ubuntu Server 11.10**，之後按下Select

<img src="https://lh5.googleusercontent.com/-wmx8zWDjMBU/UI-FQzGdbkI/AAAAAAAAByk/903ECWkyYVc/s1082/2012-10-30_144823.jpg" />

選完要的系統以後，這邊會看到有個選項 **Number of Instances** 代表的是你要建立的主機數量，因為免費的計畫每個月只有提供750小時，所以如果是開兩台的話，則是兩台的時數相加計算，這裡我們建立一台即可

另外因為是免付費，所以能選擇的 **Instance Type** 只有 **Micro(t1.micro, 613Mib)**，其他都要花錢

<img src="https://lh5.googleusercontent.com/-8EtQOn5sYIU/UI-FUrXpQZI/AAAAAAAAByw/JU14oyBEQTg/s923/2012-10-30_145517.jpg" />

再來 **INSTANCE DETAILS** 都用預設

<img src="https://lh5.googleusercontent.com/-wdMLzfYkYYs/UI-FUntOkpI/AAAAAAAABy0/0i_6vntxIXQ/s928/2012-10-30_145536.jpg" />

設定主機的標籤，在 **Value** 打上你取的名字即可

<img src="https://lh4.googleusercontent.com/-MbOIYyJvqEc/UI-FU4x1toI/AAAAAAAABy4/0J1YjC84FAE/s925/2012-10-30_145722.jpg" />

接下來這個步驟相當相當的重要，因為要建立等下登入的金鑰，自訂一個名稱，按下 **Create & Download you key Pair** ，就會下載一個金鑰檔(*.pem)，請妥善保管這個檔案，有這個檔案等下你才能透過SSH登入EC2主機

<img src="https://lh6.googleusercontent.com/-1cB05WAXDTc/UI-FWrGmNII/AAAAAAAABzI/3SldjtxLwH8/s925/2012-10-30_145856.jpg" />

防火牆群組沒有特別需求就選擇預設 **quick-start-1**

<img src="https://lh5.googleusercontent.com/-m-sDdpaLk88/UI-HR5UGR7I/AAAAAAAAB0o/HmQm9N64pqU/s873/2012-10-30_155203.jpg" />

列出一個結果清單，沒問題就按下Launch

<img src="https://lh5.googleusercontent.com/-ERYFFX--ARs/UI-FXp1zUYI/AAAAAAAABzY/9tcXui8NhvY/s914/2012-10-30_150423.jpg" />

回到AWS後台，點選左邊的Instance，你會看到主機的狀態

<img src="https://lh4.googleusercontent.com/-4tlmBtCA4XQ/UI-FYCQUe0I/AAAAAAAABzg/BzOz1XOpx8Y/s873/2012-10-30_150714.jpg" />

底下有個Public DNS，稍後建立連線時會用到Public DNS

<img src="https://lh5.googleusercontent.com/-Q7z3TcmKTvw/UI-FZXjHSTI/AAAAAAAABzo/WC8BPmzR13A/s1222/2012-10-30_151020.jpg" />

接下來就要開始連到我們的EC2虛擬機器，必須透過SSH軟體來遠端登入，Windows大部分都是使用 **Putty** ， 不過因為因為EC2的金鑰是以.pem檔來儲存，Putty無法直接使用，所以要用一個叫做 **Puttygen** 來做金鑰的轉檔

<a href="http://the.earth.li/~sgtatham/putty/latest/x86/putty.exe" target="_blank">Putty 下載點</a>

<a href="http://the.earth.li/~sgtatham/putty/latest/x86/puttygen.exe" target="_blank">Puttygen 下載點</a>

執行 **puttygen.exe** 且無需安裝，打開後按下 **Load**，選擇剛才下載的.pem檔

<img src="https://lh3.googleusercontent.com/-pdtYelILnZo/UI-FbRF5hQI/AAAAAAAABzw/BAS6tI_xdEk/s496/2012-10-30_152801.jpg" />

選擇 **Sace private key**，存成一個 .ppk檔

<img src="https://lh6.googleusercontent.com/-1UG_P7Wqw-g/UI-FdpNAfRI/AAAAAAAABz8/T0TRFtxMVVY/s495/2012-10-30_152856.jpg" />

接著執行剛剛下載的 **Putty.exe** ， 左方選擇 **Connection** → **SSH** → **Auth** ，然後按下 **Browse** 選擇剛剛儲存的.ppk檔

<img src="https://lh4.googleusercontent.com/-sQRc74011W4/UI-FdcvHmrI/AAAAAAAABz4/f8ySGHCBkWY/s466/2012-10-30_153144.jpg" />

按下左方的 **Session** ，在Host Name欄位輸入你剛才的 **Public DNS** ，連線類型(Connection type)選擇 **SSH**，按下 **Open** 就可以開始連線囉~

<img src="https://lh5.googleusercontent.com/-_Pi8UR1wsNQ/UI-FeJmaw0I/AAAAAAAAB0I/zLQMYgYx1ng/s467/2012-10-30_153603.jpg" />

在 **login as** 後面輸入 **ubuntu** 按下Enter

<img src="https://lh6.googleusercontent.com/-hLdma4Q0mBQ/UI-FefgvVOI/AAAAAAAAB0M/J11ZpqvsRjs/s675/2012-10-30_153633.jpg" />

過一會，出現輸入指令的畫面，代表成功連線到EC2主機啦~

<img src="https://lh4.googleusercontent.com/-F1v2Uh5v0CI/UI-FfPGHXQI/AAAAAAAAB0Y/sYuU9veEA-o/s676/2012-10-30_153720.jpg" />

那要怎麼把主機關掉不用呢?

回到剛剛的EC2後台，在主機的那一欄的狀態列按下右鍵，會看到四個狀態

<img src="https://lh5.googleusercontent.com/-qyQ7NRYxMjg/UI-MfJ_bKoI/AAAAAAAAB1M/xHplgqf1hhQ/s538/2012-10-30_161427.jpg" />

**Terminate:** 代表終止，會將主機刪除

**Reboot:** 代表重新開機

**Stop:** 代表關機

**Start:** 代表開機

記住，只要一開機就會開始用一小時來計算，免費的一個月只有750小時，超過要收錢喔！

那如果想看目前總共花了多少錢，該去哪看呢?

在右上角點擊名稱，點選 **Account Activity**

<img src="https://lh4.googleusercontent.com/-4ZmMEDZjsE4/UI-Nm_7PFfI/AAAAAAAAB1U/RZEJGKYuGoU/s363/2012-10-30_161809.jpg" />

拉到最下面就可以看到囉~

<img src="https://lh3.googleusercontent.com/-zwSmA7ZkDew/UI-NnYpkmpI/AAAAAAAAB1c/_Bnh80-i0Ds/s778/2012-10-30_161909.jpg" />

接下來如果還有玩出甚麼心得，再跟大家分享~

備註:

免費使用上限

750小時的EC2 Linux Micro Instance使用(613MB RAM, 32/64位元平台) 

5GB的S3儲存空間(兩萬次下載/兩千次上傳)，30GB的網路總流量(上傳/下載各15GB)

25小時的Amazon SimpleDB使用及1GB的儲存空間 ※如果你的使用超過以上用量，則超出部份必須收費

以上內容以官方公告為主


參考資料:

<a href="http://blog.soft.idv.tw/?p=823" target="_blank">什麼是雲端服務？阿正老師教你免費玩Amazon EC2雲端主機！(上篇)</a>

<a href="http://blog.soft.idv.tw/?p=824" target="_blank">阿正老師教你免費玩Amazon EC2雲端主機(下篇)：主機實戰篇</a>

很多大大的指導

內容如有錯誤，歡迎指正