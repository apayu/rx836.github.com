---
layout: post
title: "[jQ-Plugin] 簡易的數值格式化-Numeral.js"
date: 2012-12-04 12:34
comments: true
categories: jQ-Plugin
---

對於將數字或是文字做格式化一直都覺得很阿雜，例如將算出來的數字加個千分位的逗點，或是加個貨幣符號，雖然自己做並不難，但還是希望可以有個plugin能做到這些事情，所以今天就來筆記 Numeral.js  這款plugin

<!--more-->

##Start

用法很簡單容易，先下載 <a href="http://numeraljs.com/" target="_blank">Numeral.js</a>


接著載入到網頁裡面後，js的寫法如下

	var string = numeral(1000).format('0,0');
	// 1,000
	
這樣子把數字丟進去以後，在 **format()** 傳入相對應的格式，就可以擁有千分位的逗點，其它還有


###名次
	
	var string = numeral(12).format('0o');
	//12th
	
###貨幣符號

	var string = numeral(1001).format('$ 0,0[.]00');
	//$ 1,001

###Bytes

	var string = numeral(7884486213).format('0.0b');
	//7.3GB
	
###百分率

	var string = numeral(0.974878234).format('0.000%');
	//97.488%
	
###時間

	var string = numeral(238).format('00:00:00');
	//0:03:58
	
###Unformat

能轉換過去，當然也可以轉換回來

	var string = numeral().unformat('12th');
	//12

###加減乘除

	var number = numeral(1000);

	var added = number.add(10);
	// 1010

這功能我是覺得有點多餘XD，去看source也只是做加減乘除，不太需要再多此一舉

## source code

因為最近想自己嘗試練習多寫一些plugin，所以會去觀摩別人的寫法，numeral.js是一個蠻簡單明瞭的範例，所以大概抓幾個重點出來筆記心得，有興趣的人可以一起看看XD

1.建立一個名為Numeral的函式

數值就是從這邊傳入

	// Numeral prototype object
	function Numeral (number) {
		this._n = number;
	}
2.加入一些prototype

	numeral.fn = Numeral.prototype = {

        clone : function () {
            // ...
        },

        format : function (inputString) {			
            // ...
        },
		
		// ...
		// ...

        multiply : function (value) {
            // ...
        },

        divide : function (value) {
            // ...
        },

        difference : function (value) {
            // ...
        }

    };
	
以上兩個為程式的主體，所以有了這個架構我們就可以這樣寫

	numeral(1000).format('0,0');
	
3.其它大部分就是函式的處理

	function formatNumeral (n, format) {
        var output;

        // figure out what kind of format we are dealing with
        if (format.indexOf('$') > -1) { // currency!!!!!
            output = formatCurrency(n, format);
        } else if (format.indexOf('%') > -1) { // percentage
            output = formatPercentage(n, format);
        } else if (format.indexOf(':') > -1) { // time
            output = formatTime(n, format);
        } else { // plain ol' numbers or bytes
            output = formatNumber(n, format);
        }

        // return string
        return output;
    }

會發現傳入的參數為 **n** 和 **format**

n就是 **Numeral函式** 本身，裡面帶有傳入的數值和prototype這些東西

format就是要進行什麼樣的格式化

如果format裡面含有$就是要進行貨幣的格式化，有%就是要進行百分比的格式化，其它以此類推

###參考資料:

<a href="https://github.com/adamwdraper/Numeral-js" target="_blank">Github Numeral-js</a>

<a href="http://numeraljs.com/" target="_blank">Numeral.js</a>

內容如有錯誤，歡迎指正

	

	


