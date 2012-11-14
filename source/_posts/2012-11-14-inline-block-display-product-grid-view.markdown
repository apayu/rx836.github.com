---
layout: post
title: "[CSS] 用inline-block做產品展示頁並且擁有RWD效果"
date: 2012-11-14 14:09
comments: true
categories: CSS
---

<img src="https://lh6.googleusercontent.com/-CMJtAWKTc9c/UKNLl-e4eMI/AAAAAAAAB6c/lFZ01h2vX2k/s975/inline-block-screenshot-1.png" />

相信大家對於這樣的排版並不陌生，這是一個產品的展示頁，文章參考<a href="https://twitter.com/randyhoyt" target="_blank">Randy Hoyt</a>教你如何用inline-block來做設計排版，內容簡單易懂

<!--more-->

首先先來認識一下「inline」、「block」、「inline-block」

### display : inline

像&lt;img&gt;、&lt;span&gt;、&lt;a&gt;預設的display屬性是inline，在網頁上呈現時並不會換行，且不能設定「width」、 「height」 、 「background-image」

### display : block

像&lt;div&gt;、&lt;p&gt;、&lt;h1&gt;預設的display屬性是block，只要碰到這類元素不管前後都會換行，且預設寬度為最大，但可以設定「width」、 「height」 、 「background-image」等值

### display : inline-block

從字面上可以很清楚的知道，可以同時擁有inline不會換行的特性，還可以像block一樣設定「width」、 「height」 、 「background-image」等值

OK，接下來在寫HTML之前先用小畫家做一張尺寸為200*300的圖當作產品圖

<img src="https://lh4.googleusercontent.com/-_1vY5kEq_nY/UKNMlBPDb4I/AAAAAAAAB6w/0KCoHR7sGUU/s300/a.jpg" />

接著是HTML部分

	<ul class="products">
		<li>
			<a href="#">
				<img src="a.jpg">
				<h4>內衣</h4>
				<p>$200.00</p>
			</a>
		</li>
		<li>
			<a href="#">
				<img src="a.jpg">
				<h4>冬天超級無敵霹靂保暖的阿爾卑斯山羊毛羽絨超薄大衣</h4>
				<p>$2.00</p>
			</a>
		</li><!-- more list items -->
	</ul>
	
CSS部分

	ul.products li {
		width: 200px;
		display: inline-block;
	}

呈現如下

<img src="https://lh3.googleusercontent.com/-9nRQw7JS9cU/UKNLk9c2M2I/AAAAAAAAB6I/duH5hR67EQI/s530/c1.jpg" />

會發現好像有點不太對齊，可以使用「vertical-align」CSS屬性

	ul.products li {
		width: 200px;
		display: inline-block;
		vertical-align: top;
	}

<img src="https://lh5.googleusercontent.com/-ak-BlgPF5_o/UKNLk16TvvI/AAAAAAAAB6M/LvJzebhF70o/s533/c2.jpg" />	

這樣就可以垂直靠上，不過這裡有個問題，會發現明明我沒設定margin或是padding的屬性，為啥中間會有留白，難道有預設值？其實不是，是因為剛剛在HTML的部分中間留白的關係，也就是說如果在HTML碼部分，在兩個inline-block元素之間有空白的話，會被**顯示出來**，所以為了避免這樣的情形發生，可以改成這樣

	<ul class="products">
		<li>
			<a href="#">
				<img src="a.jpg">
				<h4>內衣</h4>
				<p>$200.00</p>
			</a>
		</li><li>
			<a href="#">
				<img src="a.jpg">
				<h4>冬天超級無敵霹靂保暖的阿爾卑斯山羊毛羽絨超薄大衣</h4>
				<p>$2.00</p>
			</a>
		</li><!-- more list items -->
	</ul>
	
呈現如下

<img src="https://lh3.googleusercontent.com/-A1Un01aXcu4/UKNLlJcCU-I/AAAAAAAAB6Q/hwInTSC84nw/s535/c3.jpg" />

## Responsive

這樣的寫法還有個好處，就是他擁有最近很火紅的RWD(Responsive Web Design)效果，會依照畫面尺寸大小進行換行

<img src="https://lh5.googleusercontent.com/-sUEPvofcsWQ/UKNLl8K_OSI/AAAAAAAAB6g/82TRXLL6RyA/s845/c4.jpg" />

但世界並不會這麼完美...，每件事情總是會有缺點，這種寫法在大部分的瀏覽器上都可以執行，但IE6和IE7上面會有一些問題，所以如果想要支援較舊的瀏覽器，可以用Hack來解決

	ul.products li {
		width: 200px;
		display: inline-block;
		vertical-align: top;
		*display: inline;
		*zoom: 1;
	}

文章裡面還有提到為什麼不用Float來排版，作者說當高度一致的時候用Float是沒有問題，可是當每個項目高度不一樣的時候，就會出現**重疊**的狀況發生
	
參考資料:

<a href="http://blog.teamtreehouse.com/using-inline-block-to-display-a-product-grid-view" target="_blank">Using inline-block to Display a Product Grid View</a>

<a href="http://blog.xuite.net/vexed/tech/29221717-CSS+%E5%B1%AC%E6%80%A7+display+%E7%9A%84%E5%80%BC+inline+block+inline-block+none" target="_blank">CSS 屬性 display 的值 inline block inline-block none</a>

內容如有錯誤，歡迎指正