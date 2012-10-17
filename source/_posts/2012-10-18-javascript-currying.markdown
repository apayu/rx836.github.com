---
layout: post
title: "[JavaScript] 如何保留重複參數的函式，不必每次傳遞-Currying"
date: 2012-10-18 00:01
comments: true
categories: JavaScript
---

有時候我們呼叫某個函式，傳入的參數大多數都是一樣，那我們就可以嘗試保留那些重複的參數，而這個過程就是Currying(Curry化)

<!--more-->

Curry這個命名是一個來自<a href="http://en.wikipedia.org/wiki/Haskell_Curry" target="_blank">Haskell Curry</a>的數學家的名字所命名，Currying是一種轉換過程，至於該怎麼轉換，後面會跟著介紹，我們先來看看以下這段程式碼

	function m(x, y){
		return x * y;
	}
	
這是一段很普通的函式，傳入參數x和y以後做相乘，並且將結果回傳，可是假如有一個情況是，x參數是固定的，y值是動態的，那我們每次呼叫會怎麼做呢？

	m(2,1);
	m(2,2);
	m(2,3);
	m(2,4);
	...
	
這樣看起來雖然不太好，但尚且還可以接受，但如果函式的參數不止兩個呢？

	function m(x, y, z, p, k, l){
		return x * y * z * p * k * l;
	}

然後呼叫的時候，只有l參數變動，其他參數每次都固定...

	m(2,3,4,5,6,1);
	m(2,3,4,5,6,2);
	m(2,3,4,5,6,3);
	m(2,3,4,5,6,4);
	...

這時候就會覺得，一定有什麼方法可以更簡化，少打更多的code，這時候就要將函式進行Currying，首先我們要先寫一個泛用的Currying函式

	function currying(fn){
		var slice = Array.prototype.slice,
			stored_args = slice.call(arguments, 1);
		return function(){
			var new_args = slice.call(arguments),
				args = stored_args.concat(new_args);
			return fn.apply(null, args);
		};
	}
	
然後接著寫

	function m(x, y){
		return x * y;
	}

    var new_m = currying(m, 5)​;
    new_m(4);
	new_m(5);
	new_m(6);
	
這樣y值不管傳什麼，x值一樣都保持固定的5，程式有點複雜，現在我們就來看看吧，首先來看看變數slice和stored_args分別是什麼

	function currying(fn){
        var slice = Array.prototype.slice,
            stored_args = slice.call(arguments, 1);
        console.log(slice); //function slice() { [native code] }		
        console.log(stored_args); // [5] 		
    }
    
    function m(x, y){
        return x * y;
    }

    currying(m, 5);​
	
我們可以看到，變數slice存放<a href="http://www.w3school.com.cn/js/jsref_slice_string.asp" target="_blank">slice()</a>方法，因為我們想要將傳進來的參數轉換成陣列，並且將第一個參數去掉(這裡指的第一個參數就是m())，所以最後只剩下一個5的陣列

	console.log(stored_args); // [5]
	
接著後面會return一個函式，函式將會重複的參數存在裡面，等於回傳一個新的函式讓User使用，從console.log可以看到變數new_args和args

	function currying(fn){
        var slice = Array.prototype.slice,
            stored_args = slice.call(arguments, 1);
        return function(){
            var new_args = slice.call(arguments),
                args = stored_args.concat(new_args);
            console.log(new_args);//[4] 
            console.log(args);//[5, 4] 
            return fn.apply(null, args);
        };
    }
    
    function m(x, y){
        return x * y;
    }

    var new_m = currying(m, 5);
    new_m(4)
​
回傳的函式會放在變數new_m，而這個函式到底在做些甚麼呢？其實就是將新得到的參數(也就是從new_m(4)傳進來的那個4)取出，接著利用concat將新參數和舊參數合在一起，再將合在一起後的參數([5, 4])丟進當初m()這個函式裡面，達成原本要相乘的任務，這樣當函式的參數一多，重複性高時，就可以做優化，例如就如同類似之前提到的y、z、k皆為重覆值，x值為動態

	function currying(fn){
		var slice = Array.prototype.slice,
			stored_args = slice.call(arguments, 1);
		return function(){
			var new_args = slice.call(arguments),
				args = stored_args.concat(new_args);
			return fn.apply(null, args);
		};
	}
	
	function m(x, y, z, k){
		return x * y * z * k;
	}

    var new_m = currying(m, 5, 6, 7)​;
    new_m(4);
	new_m(5);
	new_m(6);
	
重複的事情被取代了，這樣程式碼是不是看起來優化了呢？

參考資料:

<a href="http://www.books.com.tw/exep/prod/booksfile.php?item=0010538538" target="_blank">JavaScript 設計模式</a>

內容如有錯誤，歡迎指正