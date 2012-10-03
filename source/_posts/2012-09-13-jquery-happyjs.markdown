---
layout: post
title: "[jQuery] 快樂的Happy.js"
date: 2012-09-13 15:45
comments: true
categories: jQuery
---

今天看到有人分享<a href="http://happyjs.com/" target="_blank">Happy.js</a>，因為名字的關係引起了我的興趣，好奇的想說用這個plugin是不是寫起來很快樂，所以決定來玩一下

<!--more-->

事實證明...，其實並沒有特別Happy，當然這只是取名字而已XD，Happy.js其實是一套驗證表單的plugin，官方網站強調的是它相當的輕量且容易擴充，而實際檔案大概也只有3kb左右，用法也相當的簡單

首先一樣是引入js部分，分別是jQuery和happy.js還有happy.methods.js，可以直接下載<a href="http://github.com/andyet/Happy.js/zipball/master" target="_blank">範例檔</a>

	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.8.1/jquery.min.js"></script>
	<script src="happy.js"></script>
	<script src="happy.methods.js"></script>
	
happy.js是主程式，happy.methods.js是一些擴充的驗證方法

接著是HTML部分

	<form id="awesomeForm" action="/lights/camera" method="post">
      <input id="yourName" type="text" name="name" />
      <input id="email" type="text" name="email" class="" />
      <input type="submit" value="go" />
    </form>
	
再來就是js部分

	$('#awesomeForm').isHappy({
		fields: {
		  '#yourName': {
			required: true,
			message: '忘記填姓名囉！'
		  },
		  '#email': {
			required: true,
			message: '忘記填Email囉！',
			test: happy.email 
		  }
		}
	  });
	  
其實蠻好理解的，主要就是fields裡面要設置需要驗證的欄位，例如像#yourName和#email的input，然後message就是看要出現甚麼錯誤訊息，test這個屬性就是指擴充的驗證方法部分，就是寫在剛剛引用的happy.methods.js裡面，所以你可以除了要求不能空白以外，還可以進一步要求Email的格式

而出現的錯誤訊息就如同下面所示

	<span id=​"textInput1_unhappy" class=​"unhappyMessage">​忘記填Email囉！​</span>
	
這個span會在發生錯誤時添加，而你會看到類別就叫**unhappyMessage**，作者就說他是認真的，不是開玩笑的，因為這真的不是個很開心的訊息 XD

所以你可以添加一些unhappyMessage的CSS樣式讓錯誤訊息更顯著

當然這不一定只能用在表單部分，如果有時候不是一個FORM而是用div所拼湊的表單，要做AJAX的效果，就可以把預設的submitButton改掉，如下所示

	$('#awesomeForm').isHappy({
		fields: {
		  '#yourName': {
			required: true,
			message: '忘記填姓名囉！'
		  },
		  '#email': {
			required: true,
			message: '忘記填Email囉！',
			test: happy.email 
		  }
		},
		submitButton:'#subBtn' //自己制定的submitButton
	});
	  
不過我後來發現一個小問題，如果是制定的話，再驗證完後要觸發AJAX卻不知道要寫哪裡，所以我後來自己稍微修改了一下原始碼，把要加到AJAX的部分寫在happy.js裡面

	function handleSubmit() {
      var errors = false, i, l;
      for (i = 0, l = fields.length; i < l; i += 1) {
        if (!fields[i].testValid(true)) {
          errors = true;
        }
      }
      if (errors) {
        if (isFunction(config.unHappy)) config.unHappy();
        return false;
      } else if (config.testMode) {
        if (window.console) console.warn('would have submitted');
        return false;
      } else {          //這個else是後來自己加上去的
		                //代表通過驗證以後要做的事情，把AJAX的code寫在這裡
	  }					//
    }
	
當然也可以把這個修改寫得更好看一些，但我用最快的方式來補充這個AJAX的需求

如有錯誤，歡迎指正