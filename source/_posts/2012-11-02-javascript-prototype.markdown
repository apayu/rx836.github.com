---
layout: post
title: "[JavaScript] prototype與建構函式和物件"
date: 2012-11-02 15:11
comments: true
categories: JavaScript
---

今年開始陸陸續續的開始參加一些讀書會，其中有一本是關於HTML5，裡面有些章節是談到JavaScript，剛好我導讀其中一章講關於自定物件方面，那就趁著這個機會再把JavaScript的觀念整理清楚，增強自己的功力，尤其是一直很模糊的「prototype」

<!--more-->

在講prototype之前，要先複習一下之前所寫的 <a href="http://blog.rx836.tw/blog/javascript-patterns-1/" target="_blank">[JavaScript] 談物件, 實字與建構式</a> 和 <a href="http://blog.rx836.tw/blog/javascript-custom-function/" target="_blank">[JavaScript] 建立物件的第三招-自訂建構式函式</a>，這兩篇文章有提到物件和建構式函式(constructor functions)，但其實還有一個叫做prototype也跟他們兩個糾纏不清，形成特殊的三角關係(誤)

首先我們先來看物件

	var obj={
		name : '阿帕',
		run : function(){
			//跑跑跑
		}
	}
	
	console.log(obj.name);
	//阿帕
	obj.run();
	//執行裡面的跑跑跑
	
OK，相信大家對上面這個物件不陌生，但除了以上建立物件的方法，還可以用建構式函式

	function Obj(){
		this.name = '阿帕';
		this.run = function(){
			//跑跑跑
		}
	}
	
	var _obj = new Obj();
	console.log(_obj.name);
	//阿帕
	_obj.run();
	//執行裡面的跑跑跑
	
所以我們可以說，JavaScript利用**建構式實例出一個物件**，那跟prtotype有甚麼關係呢？

其實在建構式函式裡面有個屬性叫做prototype，他就是建構式函式的「原型物件」

	function Obj(){
		this.name = '阿帕';
		this.run = function(){
			//跑跑跑
		}
	}
	
	console.log(Obj.prototype);
	//Obj {} 這也是一個物件，叫原型物件
	
這個原型物件可以做什麼呢？假如我今天用Obj()這個建構式函式實例了a、b、c三個物件，完成以後我還要每個都再加一個屬性height怎麼辦？你可能會這樣寫

	function Obj(){
		this.name = '阿帕';
		this.run = function(){
			//跑跑跑
		}
	}
	
	var a = new Obj();
	var b = new Obj();
	var c = new Obj();
	
	//為每個物件增加屬性
	a.height= 15;
	b.height= 15;
	c.height= 15;
	
但其實你可以這樣寫

    function Obj(){
        this.name = '阿帕';
        this.run = function(){
            //跑跑跑
        }
    }
    
	var a = new Obj();    
    Obj.prototype.height = 15;
    var b = new Obj();    
	var c = new Obj();    
	
	
    console.log(a.height);
	console.log(b.height);
	console.log(c.height);
	
有發現我只要給建構函式Obj的prototype屬性，從Obj實例出來的物件都有相同的屬性，而且不管是先實例出來的a還是後面實例出來的b、c都一樣擁有

為什麼在原型物件Obj.prototype裡面增加屬性，會影響到從Obj建構式裡面實例出來的物件呢？

原來是因為建構函式Obj的屬性prototype是原型物件Obj.prototype，但Obj.prototype裡面也有一個屬性叫做constructor又指回建構函式Obj，所以當Obj.prototype增加屬性的時候，就會連帶增加從建構式函式Obj實例出來的物件
	
	Obj === Obj.prototype.constructor
	
不知道這樣說明，大家清楚嗎:)

參考資料:

自已

內容如有錯誤，歡迎指正


	