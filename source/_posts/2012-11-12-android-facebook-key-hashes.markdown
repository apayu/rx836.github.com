---
layout: post
title: "[PhoneGap] Android開發Facebook取得Key Hashes"
date: 2012-11-12 11:38
comments: true
categories: PhoneGap Facebook
---

之前曾經有寫過一篇關於Facebook web App開發的<a href="http://blog.rx836.tw/blog/facebook-app-create-getfbid/" target="_blank">心得文章</a>，但如果是用PhoneGap來開發Facebook App呢？我想很多人第一個遇到的問題就是，我在Facebook開發者設定是註冊web還是Android？

<!--more-->

一開始我也為這個問題困擾一陣子，但後來仔細想想PhoneGap的原理，在看看Facebook 開者人員的設定，答案就呼之欲出

<img src="https://lh4.googleusercontent.com/-Us90e1j38QY/UKCWPyT6CtI/AAAAAAAAB5k/XDg4FiqkaYo/s831/a2.jpg" />

可以看到不管是Website with Facebook Login還是App on Facebook都要輸入網址部分，可是手機的APP沒有網址這部分(我的認知.. 有錯煩請指正)，而且PhoneGap最後還是用手機App包裝起來，所以說到底，他骨子裡還是個手機App

不過這就讓我第一次接觸到Android開發的人撞到牆了，因為我根本就不知道什麼是「Key Hashes」，也不知道應該怎麼取得這個值，所以就上網做了一些功課，整理出一些心得給大家做參考

Key Hashes最主要就是讓Facebook分辨你的App是不是當初設定的那支App，要符合才能對Facebook API進行存取，產生Key Hashes方法如下

1.首先下載<a href="http://sourceforge.net/projects/gnuwin32/files/openssl/0.9.8h-1/openssl-0.9.8h-1-bin.zip/download?use_mirror=nchc" target="_blank">OpenSSL</a>

2.將openssl.exe這個檔案放到C:\Program Files\Java\jre6\bin這個資料夾裡面

3.用**系統管理員身分**將cmd.exe打開，並且開始製作「keystore」，語法如下

	keytool -genkey -v -keystore apa.keystore -alias apa -keyalg RSA -keysize 2048 -validity 10000
	
請注意，程式碼中「apa.keystore」和「apa」是自取的名稱，你也可以叫做「abc.keystore」和「abc」

每個指令的名稱意思分別為:

-keystore：名稱

-alias：別名

-keyalg：演算法

-validity：有效天數

<img src="https://lh5.googleusercontent.com/-DHMUBhM3hrI/UKCWP5a59pI/AAAAAAAAB5g/SKPFMSolbjI/s679/a3.jpg" />

4.產生「keystore」以後，開始取得Hash Key，語法如下

	keytool -exportcert -alias apa -keystore apa.keystore | openssl sha1 -binary | openssl base64
	
一樣注意-alias和-keystore的名稱是剛剛自己取的名稱

最後就會看到類似以下的代碼在視窗上顯示出來

	P1suAlHZ3f8RkLibv4MnnI3z2fg=
	
這樣代表你已經成功取得Hash Key囉，將這組Key貼到Facebook開發者人員設定App的地方，大功告成！

參考資料:

<a href="http://wazai.net/1921/android%E4%BD%BF%E7%94%A8facebook-sdk%E7%94%B3%E8%AB%8B%E7%AF%87" target="_blank">Android使用Facebook SDK(申請篇)</a>

<a href="http://wangshifuola.blogspot.tw/2011/06/androidfacebook-sdkpart1.html" target="_blank">Android學習_使用facebook sdk_Part1準備</a>

<a href="http://wangshifuola.blogspot.tw/2011/06/androidgoogle-map-api-key.html" target="_blank">Android學習_如何申請Google Map API Key(實機用)</a>

內容如有錯誤，歡迎指正