---
layout: post
title: "[學習筆記] 簡單容易，如何在VM裝Windows 8來玩玩[一]"
date: 2012-09-21 17:37
comments: true
categories: 
---

因為想參加Microsoft的<a href="http://www.microsoft.com/taiwan/promo/Win8AppFest/">Apps開發者聯盟</a>，但其實是想拼前100名就可以得到快手獎XD，獎品是Windows 8 專業版軟體乙套，所以想來挑戰看看，但要先把windows 8安裝起來，所以這篇紀錄一下安裝過程，用的是VM

<!--more-->

當然前提你必須先把VM給裝起來，網路上<a href="http://blog.xuite.net/yh96301/blog/53120472" target="_blank">教學還蠻多的</a>，這篇就不多加闡述

一開始首先要去下載微軟所推出的<a href="http://windows.microsoft.com/en-US/windows-8/iso" target="_blank">Windows 8 Consumer Preview(消費者預覽版)</a>，直接下載32-bit (x86)這個版本就可以，但只有English版本，下載完後開啟VM

### 2012/09/25 補充

更正一下，如果是要開發Windows 8的應用程式，應該要安裝<a href="http://msdn.microsoft.com/zh-TW/evalcenter/jj554510.aspx" target="_blank">Windows 8 evaluation for developers</a>，這裡的Windows 8版本才對，不然會沒辦法安裝VS 2012開發工具...，而且還有中文版本，因為安裝程序都一樣，所以文章內容一樣可以參考

點選『Create a New Virtual Machine』

<img src="https://lh5.googleusercontent.com/-otZSLwijQ0U/UFyf4XwFSyI/AAAAAAAABkc/FNIph_J7JHs/s657/1.jpg"  />

接著點選『I will Install the operating system later』

<img src="https://lh5.googleusercontent.com/-xeiYkr8fudM/UFyf8en7F3I/AAAAAAAABls/swewFIyCkmE/s659/2.jpg"  />

作業系統選擇『Microsoft Windows』，接著再選擇『Windows 7』，因為VM沒有Windows 8可以選

<img src="https://lh3.googleusercontent.com/-_Co3ZTLZ3bA/UFygAqiA5CI/AAAAAAAABm0/UixQmOxkxiU/s657/3.jpg"  />

輸入虛擬機器的名稱，這邊取名『Windows 8』，再選擇要存放的路徑，然後點選『Next』

<img src="https://lh4.googleusercontent.com/-KRAurNJRvLk/UFygBDKQoII/AAAAAAAABm8/YwQLP43AyUQ/s658/4.jpg"  />

接著設定虛擬硬碟的大小，並且設定『Store virtual disk as a single files』，將虛擬硬碟存成一個資料夾，按下『Next』

<img src="https://lh3.googleusercontent.com/-EO-2MBYjcEc/UFygBr6bmvI/AAAAAAAABnI/5JjNmotkvEw/s656/5.jpg"  />

再來準備要來設定記憶體和掛載Windows 8映像檔，選擇『Customize Hardware…』

<img src="https://lh4.googleusercontent.com/-nbky8ASN0ck/UFygBw-01wI/AAAAAAAABnE/dxdanwgZcjg/s660/6.jpg"  />

調整記憶體，一般來說建議為實體記憶體的3分之1至2分之1之間，官方網站是說至少要1G

<img src="https://lh5.googleusercontent.com/-btOEe35_ToI/UFygCdtCjwI/AAAAAAAABnY/P6JM4vBI9Nc/s656/7.jpg"  />

接著選擇『New CD/DVD』的選項，再點『Use ISO image file:』，再按「Browse…」來選擇映像檔

<img src="https://lh6.googleusercontent.com/-WxOQRqu4nF8/UFygCyaFR9I/AAAAAAAABng/uQc30JVd0Oo/s658/8.jpg"  />

選擇好映像檔以後就按下『Close』

<img src="https://lh4.googleusercontent.com/-v5ICos8qLUQ/UFygC-8bVNI/AAAAAAAABnc/9rp1LeXOO8I/s661/9.jpg"  />

最後按下『Finish』就新增了一個虛擬機器

<img src="https://lh6.googleusercontent.com/-5QYBPsTQNwA/UFyf4pX33AI/AAAAAAAABkg/5rhtXII6H1s/s657/10.jpg"  />

按下『Play virtual machine』，開始來進行安裝囉！

<img src="https://lh5.googleusercontent.com/-G0VcZ28gqbA/UFyf4laUtKI/AAAAAAAABkk/jvgPOqPFaOE/s659/11.jpg"  />

因為篇幅有點過長，為了方便閱讀，所以分成兩篇來記錄

參考資料:

<a href="http://blog.xuite.net/yh96301/blog/58183942" target="_blank">VMware Player 4.0安裝Windows 8消費者預覽版本(一)</a>

如有錯誤，歡迎指正

