---
layout: post
title: "twitter-bootstrap"
date: 2012-10-01 18:41
comments: true
categories: 
---

<a href="http://twitter.github.com/bootstrap/" target="_blank">Twitter Bootstrap</a>越來越多人在用了，當然最主要的原因就是他可以幫助網頁開發者快速的開發出，有不錯外觀的web或是mobile apps，這對於許多不擅長外觀設計的網頁工程師們(包括我)，可以說是省下不少煩惱Layout的麻煩，不僅如此，針對按鈕、表格、或是排版，Bootstrap都幫你處理的好好，只要簡單幾個步驟引入即可

<!--more-->

首先要先下載<a href="http://twitter.github.com/bootstrap/getting-started.html" target="_blank">Bootstrap</a>，你可以選擇compil過後的，或是選擇source版本，Bootstrap的css是用Less寫的，所以如果你想修改細節部分，可以下載source版本，一般來說直接用compiled版本即可

接著就會看到有三個資料夾(css & js & img)

<img src="https://lh3.googleusercontent.com/-RHqEXjgftnI/UGl5vs7qyaI/AAAAAAAABoU/tKc440KDt5Y/s872/a.jpg" />

可以把他們全部放入你的專案裡面，但引入到html時，css和js就只要選擇有沒有壓縮過的版本就好，然後接下來就可以開始使用了！但請注意還是要引入jQuery喔，接下來就是介紹一些使用範例

## Base CSS examples

### Buttons

	<button class="btn dropdown-toggle" data-toggle="dropdown">Action <span class="caret"></span></button> <button class="btn btn-primary dropdown-toggle" data-toggle="dropdown">Action <span class="caret"></span></button> <button class="btn btn-danger dropdown-toggle" data-toggle="dropdown">Danger <span class="caret"></span></button> <button class="btn btn-warning dropdown-toggle" data-toggle="dropdown">Warning <span class="caret"></span></button> <button class="btn btn-success dropdown-toggle" data-toggle="dropdown">Success <span class="caret"></span></button> <button class="btn btn-info dropdown-toggle" data-toggle="dropdown">Info <span class="caret"></span></button> <button class="btn btn-inverse dropdown-toggle" data-toggle="dropdown">Inverse <span class="caret"></span></button>



