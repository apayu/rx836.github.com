---
layout: post
title: "[JavaScript] 建立物件的第三招-自訂建構式函式"
date: 2012-09-11 00:43
comments: true
categories: JavaScript
---

在前面一篇文章<a href="http://blog.rx836.tw/blog/javascript-patterns-1/" target="_blank">[JavaScript] 談物件, 實字與建構式</a>，裡面有講到關於物件的建立，不過礙於篇幅，只談到**實字模式(literal patterns)**和**建構式函式(constructor functions)**，但其實還有一個建立物件的方法，那就是**自訂建構式函式**

<!--more-->

用自定義的建構式函式來建立物件，直接用範例來說明

	var kitty = new Cat('Kitty');
	var kitty.say(); // "kitty:喵~"
	
跟之前的建構式不同的地方在於，之前是用內建的new Object()，這裡我們是用new Cat()，這種模式很像Java使用一個class Cat來建立物件，語法非常的相似，但其實JavaScript並沒有class，Cat只是一個函式

Cat的建構式定義如下

	var Cat = function (name){
		this.name = name;
		this.say = function(){
			return name+":喵~";
		}
	};
	
但其實真正背後運作的方式是這樣，註解為JavaScript實際上還有做一些我們看不到的事情

	var Cat = function (name){
	
		//建立物件實字, 一個空物件
		//var this = {};
		
		//接著替this加入屬性和方法
		this.name = name;
		this.say = function(){
			return name+":喵~";
		}
		
		//最後return this
	};
	
整個的流程首先會建立一個空物件，參考至this變數，藉由this的參考，將屬性和方法加入到此物件(this)，最後再將物件隱含的回傳出去(這邊要注意的是，回傳的情況是假設**沒有其他物件被明確的指定回傳**，後面則會提到)

範例中say()是直接加入至this，不過真正實務中，當你每次new Cat()的時候，就會建立一個新函式到記憶體裡面，很明顯的會浪費記憶體效能，所以最好的方式是加入到原型(prototype)中

	//只可以重複利用，都應該放進原型裡面
	Cat.prototype.say = function(){
		return this.name+":喵~";
	};
	
不過這裡有個問題，假如忘記加上new會發生甚麼事情？其實是不會有語法或執行上的錯誤，但卻會導致非預期的錯誤發生，因為沒有加new以後，所有的this都指向全域物件去了！(例如window)

	function cat(){
		this.name = "kitty";
	}
	
	var kitty = new Cat();
	console.log(typeof kitty); // "object" 為物件
	console.log(kitty.name);
	
	var kitty2 = Cat();
	console.log(typeof kitty2); // undefined 忘了new, 不會有物件this回傳, 變成全域
	console.log(window.name); //全域變數
	
不過為了預防這種情況發生，可以利用以下寫法

	function cat(){
		
		//還是一樣會建立一個this
		//var this = {};
		
		var _self = {};		
		_self.name = "kitty";
		
		//不過return被_self取代了
		return _self;
	}
	
所以不管User怎麼呼叫，都一定會回傳一個物件，也就是強制new的做法

	var kitty = new Cat();	
	console.log(kitty.name); // "kitty"
	
	var kitty2 = Cat();	
	console.log(kitty2.name); // "kitty"
	
參考資料:

<a href="http://www.books.com.tw/exep/prod/booksfile.php?item=0010538538" target="_blank">JavaScript 設計模式</a>

如有錯誤，歡迎指正