---
layout: post
title: "[jQ-Plugin] 輕鬆幫表格做responsive"
date: 2013-01-21 12:28
comments: true
categories: jQ-Plugin
---

因為移動設備的成長，RWD(Responsive web design)這個應用已經在許多網頁上都看的到，除了做一個專屬於 mobile 的網站設計以外，也可以讓一個網站來符合許多螢幕解析度大小，而這兩個方法的優與劣，如何選擇，就看專案當下的情況來做決定

<!--more-->

例如以文字為主的部落格或是簡單的頁面就很適合做RWD，但介面太複雜或是功能太多，建議還是另外開發專屬的獨立網站，有興趣的人可以參考這篇的 <a href="http://cssindesign.tumblr.com/post/40513264330/responsive-web" target="_blank">實作心得</a>，這邊就不討論太多

今天這篇主要介紹一個jQuery plugin，叫FooTable，利用簡單的幾行程式，就可以將網頁裡面的 table 擁有 RWD 的效果

##Start

首先要先下載 js 和 css，可以到 github 下載

<a href="https://github.com/bradvin/FooTable" target="_blank">DOWNLOAD</a>

載回來後會發現裡面有一些 js 和 css檔，還有幾個 demo 範例，但有一些檔案是看情形選擇載入，其中最主要的只有兩個檔案，分別是

footable-0.1.js 和 footable-0.1.css

在網頁裡面載入這兩支檔案和jQuery以後，接下來就來做簡單的範例

###phone和tablet

FooTable最主要會判斷三種情形，除了一般的 Desktop 以外，還分成 phone 和 tablet，開發人員可以在每個欄位中，選擇要在什麼情況底下做縮排，以下是基本的HTML

HTML部份

	<table class="footable">
      <thead>
        <tr>
          <th data-class="expand">
            姓名
          </th>
          <th>
            職業
          </th>
          <th data-hide="phone">
            年齡
          </th>
          <th data-hide="phone,tablet">
            性別
          </th>
        </tr>
      </thead>
      <tbody>
        <tr><td>小馬</td><td>司機</td><td>59</td><td>男</td></tr>			
		<tr><td>小陳</td><td>保全</td><td>42</td><td>男</td></tr>			
		<tr><td>小英</td><td>行政</td><td>27</td><td>女</td></tr>			
      </tbody>
    </table>
	
可以看到在&lt;thead&gt;底下會有 data-class 和 data-hide 兩個 HTML5 的自訂屬性，如果 data-class="expand" 設在『姓名』那個欄位，**代表的意思是會在此欄位建立 icon 圖案 『+』 和 『-』**，而 data-hide 指的是**該欄位在什麼情況下會隱藏縮排**，例如在上面範例中的年齡設為 data-hide="phone"，表示在 phone 的寬度下會觸發此事件

那或許會有人疑問，phone和 tablet 的寬度判斷依據是什麼呢？這邊可以直接打開 footable-0.1.js 這支檔案，搜尋底下這行原始碼

	options: {
      delay: 100, // The number of millseconds to wait before triggering the react event
      breakpoints: { // The different screen resolution breakpoints
        phone: 480,
        tablet: 1024
      },
	...
	...
	}
	
會發現原來 FooTable 預設屬性 phone 的寬度為480px，而 tablet 是1024，所以假設現在 Table 寬度只有 780，那擁有tablet 這個值的欄位就會做隱藏縮排，這些值都可以依照個人需求做修改，說了那麼多怕大家看不懂，那就直接來看結果圖吧

table寬度大於1024px

<img src="https://lh6.googleusercontent.com/-SenmhgVS_s4/UPz2ku3YqeI/AAAAAAAACNc/vpvMWrwVeFk/s1077/2013-01-21_152914.jpg" />

table寬度小於1024px，大於480px，**性別被縮排，姓名多了展開的圖案『+』**

<img src="https://lh6.googleusercontent.com/-AZyIxH4mZgY/UPz2kr5W8CI/AAAAAAAACNU/wDNk3hkqDNc/s823/2013-01-21_153046.jpg" />

table寬度小於480px，性別和年齡都被縮排

<img src="https://lh4.googleusercontent.com/-taApAI4ZcRk/UPz2ks5zlpI/AAAAAAAACNY/JM2RGkX-BPU/s219/2013-01-21_153224.jpg" />

點擊每一列即可展開看被隱藏的資訊

<img src="https://lh3.googleusercontent.com/-PNOSlcS6mhU/UPz2lfqAOvI/AAAAAAAACNg/jhzxH6Y5l_M/s227/2013-01-21_153321.jpg" />

是不是很方便呢？

###搜尋與排序

除了一般的 table 以外，常用到的『搜尋』和『排序』當然也不可少，FooTable貼心的地方在於已經幫你處理好這方面的需求，只要載入相關的 js 和加上自訂的 data- 屬性就可以完成所要的功能

<a href="http://themergency.com/footable-demo/demo-sorting.htm" target="_blank">Sorting demo</a>

<a href="http://themergency.com/footable-demo/demo-filtering.htm" target="_blank">Filtering demo</a>

但比較可惜的地方在於沒有實做分頁這塊，所以如果有這方面需求的朋友，可能要自己另外加上

##總結

個人覺得這款jQuery plugin做的相當簡單，使用上也十分容易，主要就是在欄位方面加上 data- 屬性，可擴展性也高，可以依照『搜尋』和『排序』的邏輯模式新增自己的功能，在縮排與顯示方面的UI設計也讓人感到實用方便，有興趣的朋友可以參考看看

###參考資料:

<a href="http://themergency.com/footable/" target="_blank">FooTable</a>

內容如有錯誤，歡迎指正



