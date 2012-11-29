---
layout: post
title: "[jQuery] jQuery常用的表單驗證事件"
date: 2012-11-29 15:40
comments: true
categories: jQuery
---

在動態網頁的世界裡面，最常使用到的大概就非Forms莫屬，填寫完表格以後都會將資料傳送到bcak-end(後端)，而在傳送之前，有一些資料的驗證都會交由front-end(前端)來處理，這篇就來紀錄一下對於HTML Forms來說，常用的一些jQuery方法

<!--more-->

##.blur()

**Blur** 發生在當一個元素失去焦點時，所觸發的一個事件，在原生的HTML裡面提供了 **onblur** 這個屬性，可以將這個事件附加到HTML元素上，範例如下

	<input type = "text" onblur = "doSomething();" />
	
當光標的焦點在input裡面以後，在點擊input以外的元素就會觸發，不過這是老舊的寫法，因為我們希望能盡量在HTML上保持乾淨，與程式邏輯做分離，所以就會使用jQuery的blur()來達到此任務

	$("input").blur(function() { /* Do something... */ } );
	
要特別注意的是 **onblur ** 這個事件適用於所有的input元素，也就是說就算是button也適用，因為在鍵盤上有個「Tab鍵」可以在網頁上做焦點的切換，就會觸發 **onblur** 這個事件

不過在1.7以後的jQuery版本裡面建議開始使用 **.on()** 來達到此任務，效能會比較好

	$('input').on('blur', function() { /* Do something.... */ });
    $('input').off('blur', function() { /* Do something... */ });
	
相較於 **.on()** ， **.off()** 就是停止監聽這個事件，善用 **.off()** 也可以讓效能增加(參考<a href="http://blog.darkthread.net/post-2011-11-07-jquery-1-7-release.aspx" target="_blank">黑暗執行緒 jQuery 1.7筆記</a>)，避免過多不必要的事件監聽

如果你只希望監聽「某個類型元素」的事件，可以這樣寫

	$("input[type=radio]").on('blur', function() { /* Do something... */ } );
	$("input[type=checkbox]").on('blur', function() { /* Do something... */ } );	
	$("input[type=text]").on('blur', function() { /* Do something... */ } );

當然，只想要針對單一指定的元素，可以用id值來選取

	$("input#Email").on('blur', function() { /* Do something... */ } );

##.change()

**change** 事件相當於HTML裡面的 **onchange ** 屬性，跟上一個討論 **blur** 事件很像，但不同的地方在於，當焦點離開元素之前，如果元素有改變的話，就會觸發這個事件，寫法如下
	
	$("input#target").change(function() { /* Do something... */ } );
    $("input#target").bind("change", function() { /* Do something... */ } );
    $("input#target").on("change", function() { /* Do something... */ } );
	
一樣建議使用 **on()** 來監聽change這個事件

同時利用 **onChange** 和 **onBlur** 來驗證表單也是很常見的做法

	
    $("input#target").on("change", EmailChecked );
    $("input#target").on("blur", EmailChecked );
	
	function EmailChecked( value )
    {
        //在這邊做驗證...
 
         if (valid)
         {
             // 驗證通過...
         }
         else
         {
             // 驗證不通過...
         }
    }
	
可以讓驗證做的更完善，兩個事件的觸發先後順序為 onChange>onBlur

##.focus()

相等同於 **onFocus** ，如果 **.blur()** 是失去焦點，那 **.focus()**就是得到焦點，也就是在某個元素被點擊以後所觸發的事件，語法如下

	$("input#myInput").focus(function() { /* Do something... */ });
    $("input#myInput").bind("focus", function() { /* Do something... */ });
    $("input#myInput").on("focus", function() { /* Do something... */ });
	
這邊還是建議使用 **.on()**

##.select()

select算是很容易讓人混淆的事件，在text input元素裡面(或textarea)，當你將文字反白以後，就會觸發此事件，範例如下

	<input type="text" value="Some text" />
	
	<script>
		$(":input").select( function () { 
			alert('文字被反白');
		});
	</script>

但有些人可能會誤用成這樣

	$("input[type=checkbox]").select();
	$("input[type=radio]").select();  
	
**這個方法並不能將checkbox或是radio執行勾選**

正確的做法應該是這樣

	$("input[type=checkbox]").prop("checked", true); // Check checkbox
    $("input[type=radio]").prop("checked", true); // Check radio button
	
##.val()

這大概是jQuery最常用到的方法之一， **.val()** 可以取得值

	var Email = $("input#Email").val();
	
當是用在&lt;select&gt;元素時，**.val()** 可以將現在選取的項目值取出來

	<select id="test1" name="test1" />
	  <option value="1">select1</option>
	  <option value="2">select2</option>
	  <option value="3">select3</option>
	</select>
	
	<script>
		$("select").val(); 
	</script>

不過 **.val()** 只適用在input元素裡面，就算在div裡面自己加上value屬性也取不到值

	<div value = "apa"></div>
	
	<script>
		$("div").val(); //錯誤的...
	</script>
	
div應該要用 **.text()** 或是 **.html()** 來修改裡面的內容

##.submit()

在表單傳送裡面，HTML必須長成這樣

	<form id = "myForm">
        <input type = "submit" value = "Submit"/>
    </form>
	
submit的button必須一定要包裹在&lt;form&gt;，如果想要藉由&lt;form&gt;以外的元素來觸發呢？可以這樣寫

	$("input#myButton").click(function() {
        $("#myForm").submit();
    });

這樣就可以不需要透過submit來將資料送出，另外想在送出前做表單驗證的話，也可以用 **.submit()**

	$("form").submit(function() {
      if ($("input:first").val() == "correct") {
        $("span").text("Validated...").show();
        return true;
      }
      $("span").text("Not valid!").show().fadeOut(1000);
      return false;
    });

當按下submit以後，就會進行驗證，假如回傳值是false，表單就不會送出

以上是常用的表單驗證方法，當然網路上也有很多寫好的plugin可以用，因為處理一大堆資料的驗證老實說蠻麻煩的，善用plugin也是個不錯的選擇，但基礎觀念還是要懂才行

###參考資料:

<a href="http://blog.darkthread.net/post-2011-11-07-jquery-1-7-release.aspx" target="_blank">黑暗執行緒 jQuery 1.7筆記</a>

<a href="http://api.jquery.com/blur/" target="_blank">jQuery API .blur()</a>

<a href="http://api.jquery.com/change/" target="_blank">jQuery API .change()</a>

<a href="http://api.jquery.com/on/" target="_blank">jQuery API .on()</a>

<a href="http://api.jquery.com/focus/" target="_blank">jQuery API .focus()</a>

<a href="http://api.jquery.com/select/" target="_blank">jQuery API .select()</a>

<a href="http://api.jquery.com/val/" target="_blank">jQuery API .val()</a>

<a href="http://api.jquery.com/submit/" target="_blank">jQuery API .submit()</a>

內容如有錯誤，歡迎指正
