---
layout: post
title: "[jQuery] 不要將任何事情都在jQuery.ready()初始化"
date: 2012-11-06 15:06
comments: true
categories: jQuery
---

Don't Initialize All the Thing in jQuery.ready()...，這是由<a href="https://twitter.com/elijahmanor" target="_blank">Elijah Manor</a>所寫的一篇文章，裡面提到不要把所有事情都放在jQuery.ready()做初始化(我就是這樣...)，現在就來筆記一下他怎麼說

<!--more-->

寫過jQuery的開發者都知道，在撰寫jQuery都會用jQuery.ready()包起來，在載入網頁時都會先等DOM載入完畢，才會執行裡面的程式碼部分，不過這有時候會讓User在進入網頁時等待過久，失去耐心，如何讓網頁在最短的時間先有畫面出來，也會影響到User使用上的經驗	

先看HTML的部分

	<form class="form-horizontal well">
		<fieldset>
			<div class="control-group">
				<label class="control-label" for="firstName">First Name</label>
				<div class="controls">
					<input id="firstName" type="text" class="input-xlarge">
				</div>
			</div>
			<!-- More HTML... -->
			<div class="control-group">
				<label class="control-label" for="birthday">Birthday</label>
				<div class="controls">
					<input id="birthday" type="text" class="date input-xlarge">
				</div>
			</div>
			<div class="form-actions">
				<button type="submit" class="btn btn-primary">Save changes</button>
				<button class="btn">Cancel</button>
			</div>
		</fieldset>
	</form>
	
這是一個很常見的表格，會填寫一些基本資料，不過為了讓User在填寫日期方便，會用「datapicker」這個jQuery UI widget來選擇日期

<img src="https://lh5.googleusercontent.com/-mb7pEbTw_FI/UJjDYpdh3oI/AAAAAAAAB28/ZQDyzYWd5K0/s296/123.jpg" />

jQuery程式碼部分

	$( document ).ready( function() {

		$( "input.date" ).datepicker({
			minDate: moment().subtract( "months", 1 ).toDate(),
			maxDate: moment().add( "months", 1 ).toDate(),
			dateFormat: "d M, y",
			constrainInput: true,
			beforeShowDay: $.datepicker.noWeekends
		});

	});
	
用這樣方式的優點是，當用戶選擇日期的時候，jQuery已經準備好並且很快的產生互動，但缺點是:

1.程式碼必須等到DOM載完才能執行

2.沒有使用context，選取器會在整個網頁進行搜尋，降低效能

3.雖然程式碼在初始化的時候就都載入完畢，但不確定是不是真的會用到

所以，為了改善這個情況，我們可以在需要的時候，在執行datapicker

	

	$( document ).on( "focus", "input.date:not(.hasDatepicker)", function() {
		toastr.info( "Initializing " + this.id );

		$( this ).datepicker({
			minDate: moment().subtract( "months", 1 ).toDate(),
			maxDate: moment().add( "months", 1 ).toDate(),
			dateFormat: "d M, y",
			constrainInput: true,
			beforeShowDay: $.datepicker.noWeekends
		});
	});
	
可以看到在「input.date」上我們監聽了一個事件「focus」，當這個元素並選取時，就會執行裡面的datapicker的UI程式，也就是說，當User要輸入日期時，才會執行這段程式碼，而不用再一開始就將程式碼執行起來

這將會讓我們的網頁不會在這麼的笨重，顯得緩慢，讓我又多學習了一招:)

參考資料:

<a href="http://www.elijahmanor.com/2012/10/dont-initialize-all-things-in.html" target="_blank">Don't Initialize All the Things in jQuery.ready() </a>

內容如有錯誤，歡迎指正




