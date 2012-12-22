---
layout: post
title: "[CSS] CSS position 觀念筆記心得"
date: 2012-12-22 11:30
comments: true
categories: CSS
---

**css position** 對於初學者來說觀念很容易混淆，我在剛學習時也很常搞不清楚relative和absolute之間的關係，但只要抓到幾個訣竅重點，其實可以很輕鬆的掌握它，這篇是紀錄我自己學習css position的心得，搭配幾個簡單易懂的範例，讓大家一起成長

<!--more-->

##Start

首先，css position 屬性共有四個值，分別為 **static**、**relative**、**absolute**、**fixed**，其中，當你沒有設定position時，預設為static，下面就來介紹這四個值的差別

###static

就如剛剛所提到的，static是預設值，意思是說，就算你沒宣告position這個屬性，默認還是為static，而通常這時候會影響到元素的位置，就是看它本身是 **block** 或是 **inline**，例如兩個&lt;div&gt;因為是block的關係，所以會上下各占據一行，那如果是兩個&lt;span&gt;，因為是inline，所以會在同一行裡面呈現

css

	#d1{
		width: 100px;
		height: 100px;
		background: blue;
	}
	#d2{
		width: 100px;
		height: 100px;
		background: red;
	}
	#s1{
			background: blue;
		}
	#s2{
			background: red;
		}	

html
	
	<div id="d1">
	div1
	</div>
	<div id="d2">
	div2
	</div>
	<span id="s1">span1</span><span id="s2">span2</span>
	
<img src="https://lh6.googleusercontent.com/-k8UTysRkMoQ/UNVYRo_fstI/AAAAAAAACGc/4eVneQSvhDg/s214/2012-12-22_120559.jpg" />

<img src="https://lh6.googleusercontent.com/-h58i2I7P0Fg/UNVYRt_asJI/AAAAAAAACGk/BkPXYijQpG0/s99/2012-12-22_120617.jpg" />

特別注意的是，static並不會受 **top**、**bottom**、**left** 和 **right** 這些屬性值影響

###relative

假如元素的position屬性值設為relative，就會受到 **top**、**bottom**、**left** 和 **right** 這些值影響所在位置，利用剛剛的範例，我們增加position屬性值和一些位移看看結果

css

	#d1{
		width: 100px;
		height: 100px;
		background: blue;
		position: relative;
		top: 20px;
		left: 20px;
	}
	#d2{
		width: 100px;
		height: 100px;
		background: red;
	}

我們在id為d1的&lt;div&gt;裡面加上了 **position: relative** 和 **top:20px** 還有 **left:20px**，會看到下面如圖的結果

<img src="https://lh5.googleusercontent.com/-brly4x9g8ck/UNVYRm2M0kI/AAAAAAAACGg/MZagmsZ8e4U/s201/2012-12-22_121717.jpg" />

藍色的div從**原本的位置**往右下角位移了，從原始位置的左上角為起點，遠離左邊(left)20px的差距，遠離上面(top)也是20px的差距，但還是保留**原本位置的空間**，並且覆蓋到d2，注意我這邊特別註明是原本的位置，因為這會跟等下介紹的 **absolute** 有所不同，那有些人或許會有疑問，可以用 **margin** 取代嗎？我們來實驗一下

	#d1{
		width: 100px;
		height: 100px;
		background: blue;
		margin-top: 20px;
		margin-left: 20px;
	}
	#d2{
		width: 100px;
		height: 100px;
		background: red;
	}
	
<img src="https://lh5.googleusercontent.com/-mWSgkOP_EZ4/UNVYSFL7X9I/AAAAAAAACGs/jU3lCto1jGM/s217/2012-12-22_122152.jpg" />

有明顯的發現，利用屬性margin做位移，元素並沒有覆蓋堆疊的問題，但會**影響到其它的元素位置**，這是要特別注意小心的地方，不可不慎

###absolute

**absolute** 跟relative很像，差別在於位移時是從哪個起始點開始算起，剛剛的relative是從原本的位置開始算，而absolute是從**整個頁面的視窗**開始算起，並且並不會保留它原本的**空間**，範例如下

	#d1{
		width: 100px;
		height: 100px;
		background: blue;
		position: absolute;;
		top: 20px;
		left: 20px;
	}
	#d2{
		width: 100px;
		height: 100px;
		background: red;
	}

<img src="https://lh5.googleusercontent.com/-gGhHTnjvx2M/UNVYSRKJwcI/AAAAAAAACGo/bqLVeZYOBok/s128/2012-12-22_123254.jpg" />

有發現藍色的&lt;div&gt;完全無視其它的元素存在，也不會干擾到其它的元素，因為它的原始空間也消失了，自己獨立起來自成一格，看起來還蠻容易了解的，不過有一個地方是初學者很容易混淆的，就是當relative和absolute一起使用時，那情形就會跟我們設想的不太一樣，範例如下

css 

	#d1{
		width: 100px;
		height: 100px;
		background: blue;
		position: absolute;;
		top: 20px;
		left: 20px;
	}
	#d2{
		width: 100px;
		height: 100px;
		background: red;
	}
	
	#d3{
		position: relative;
		width: 300px;
		height: 300px;
		border: solid 1px orange;
	}
	
html 

	<div id="d3">
		<div id="d1">
		div1
		</div>
		<div id="d2">
		div2
		</div>
	</div>
	
這裡多用一個id為d3的&lt;div&gt;包住兩個&lt;div&gt;，d3的position屬性值為relative，此時會看到藍色的&lt;div&gt;屬性值position雖然一樣是absolute，但會看到位移不太一樣了

<img src="https://lh6.googleusercontent.com/-pxPW5Q1Kocc/UNVYSScFsqI/AAAAAAAACGw/quewGWodrDc/s330/2012-12-22_124729.jpg" />

會發現藍色的&lt;div&gt;是**從id為d3的&lt;div&gt;左上角開始定位**，這代表是說，如果屬性值為absolute的&lt;div&gt;，上面還有被其它元素包住，就要注意位移計算的起始值會有所不同，那如果將relative移除的話呢?

<img src="https://lh5.googleusercontent.com/-L0jg9uoCRoI/UNVYS-iDosI/AAAAAAAACG8/_2MhBfq6cA0/s326/2012-12-22_124746.jpg" />

嗯！定位又從頁面視窗的左上角當作起始點囉，如果覺得範例感覺不到效果，可以將top和left的值加大，會更明顯

###fixed

最後講到的是fixed，它常被用於在Menu bar，位置也是受到 **top**、**bottom**、**left** 和 **right** 這些值影響，跟absolute類似，但有兩個不一樣的地方

1.它的位移起始的依據永遠都是**視窗頁面**，也就是說就算它有relative的父元素，並不會受到影響

2.它會跟著scroll移動，也就是說當畫面被往下拉時，該元素會跟隨著移到相對的位置

基於以上兩點的特色，我們就可以做出永遠固定在視窗某個地方的元素

<img src="https://lh3.googleusercontent.com/-S6zIGb8HXio/UNVYTBy6PLI/AAAAAAAACHA/y94BoXH5TO8/s1075/2012-12-22_143751.jpg" />

像是 <a href="http://pinterest.com/" target="_blank">pinterest</a> 就有用到類似的效果，不過記得要搭配 ** z-index** 來做元素堆疊

##結論

其實網路上有很多很好的文章在討論關於css position的用法和觀念，也有很多很漂亮的排版，但只要掌握好基本觀念，我相信對於那些複雜的layout也可以輕鬆的理解

另外除了上面討論的四個屬性值以外，CSS3其實還有新增另外兩個，分別叫做 <a href="http://www.w3.org/TR/css3-positioning/#center-positioning" target="_blank">position: center</a> 和 <a href="http://www.w3.org/TR/css3-positioning/#page-positioning" target="_blank">position: page</a>，不過因為非主流且各瀏覽器支援程度很低，有興趣的人在自行研究即可

###參考資料:

<a href="http://blog.teamtreehouse.com/css-positioning?utm_source=CSS+Weekly&utm_campaign=CSS_Weekly_Issue_34&utm_medium=web" target="_blank">CSS Positioning: A Comprehensive Look</a>

<a href="http://www.barelyfitz.com/screencast/html-training/css/positioning/" target="_blank">Learn CSS Positioning in Ten Steps(10個步驟學習CSS Position)</a>

<a href="http://css.1keydata.com/tw/position.php" target="_blank">CSS Position 位置</a>

內容如有錯誤，歡迎指正



