* jQuery(요소 선택자, 이벤트 리스너)

js의 라이브러리

```html
$(".btn")
jQuery.fn.init [a.btn.btn-primary, prevObject: jQuery.fn.init(1), context: document, selector: ".btn"]
0
:
a.btn.btn-primary
context
:
document
length
:
1 #하나있다
prevObject
:
jQuery.fn.init [document, context: document]
selector
:
".btn"
__proto__
:
Object(0)

$('#title') 아이디
```





첫번째 형태

`$('.btn').이벤트명(이벤트핸들러)`

`$('.btn').mouseover(function() {alert("ㄴㄴ");});`



두번째 형태(많이 사용됨)

```
$('.btn').on('mouseover',function() {

    console.log("건드리지마");

});

```



- mouse 가 버튼 위에 올라갔을때, 버튼에 있는 btn-primary 클래스를 삭제하고 btn-danger 클래스를 준다. 버튼에서 마우스가 내려왔을 때 다시 btn-danget 클래스를 삭제하고 btn-primary클래스를 추가한다.

```html 
btn = $('.btn')
btn.on("mouseenter mouseout", function() {

    if(btn.hasClass('btn-danger')){

        btn.removeClass('btn-danger').addClass('btn-primary');

    } else{

        btn.removeClass('btn-primary').addClass('btn-danger');

    }

});
```



```html
btn.on('mouseenter mouseout' , function() {
	btn.toggleClass('btn-denger').toggleClass('btn-primary');
});

// "this" 이벤트가 발생한 부분만 이벤트핸들러 실행 
btn.on('mouseenter mouseout' , function() {
	$(this).toggleClass('btn-denger').toggleClass('btn-primary');
}); 

btn.on('mouseenter mouseout' , function() {
	$(this).toggleClass('btn-denger').toggleClass('btn-primary');
	console.dir(this); html 요소 자체만
	console.dir($(this)); jQuery가 나온다.
}); 


```



hasClass

addClass

removeClass

toggleClass



* 버튼에 마우스가 오버됐을 때, 상단에 있는 이미지의 속성에 style 속성과 `width: 100px;`의 속성값을 부여한다.

```html
attr(속성, 속성값)사용
btn.on('mouseover', function(){
    $('img').attr('style','width:100px;');
});
```

* 글씨 바꾸기

```html
text() (.클래스 이름)의 text를 바꾼다.
btn.on('mouseover', function(){
    $('.card-title').text("Don't Touch me");
});
```

* 버튼(요소)에 마우스가 오버(이벤트)됐을 때(이벤트 리스너), 이벤트가 발생한 버튼($(this))과 상위 수준에 있는 요소(parent) 중에서 `.card-title`의 속성을 가진 친구를 찾아 텍스트를 변경(이벤트 핸들러)시킨다.

```html
btn.on('mouseover', function() {
	$(this).parent().find('.card-title').text("안녕");
});
siblings() 같은수준
parent() 부모수준
```



* 텍스트 변환기(오타치는 사람 놀리기)

index.html



```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>WatchaApp</title>
    <script
      src="https://code.jquery.com/jquery-3.3.1.js"
      integrity="sha256-2Kok7MbOyxpgUVvAk/HJ2jigOSYS2auK4Pfzbm7uH60="
      crossorigin="anonymous">
    </script>
    </head>
    <body>
        <textarea id = "input" placeholder = "변환할 텍스트를 입력해주세요"></textarea>
        <button class = "translate"> 바꿔줘 </button>
        <h3></h3>
        <script src="hangul.js" type="text/javascript"></script>
        <script src="translate.js"></script>
        <script type="text/javascript">
         $('.translate').on('click', function(){
           var input = $('#input').val();
           var result = translate(input);
           $('h3').text(result);
           console.log(result);
         });
        </script>
    </body>
</html>

```

translate.js

```js
function translate(str) {
  return str.split('').map(function(el){
    var d = Hangul.disassemble(el);
    if(d[3] && Hangul.isVowel(d[1]) && Hangul.isVowel(d[2])){
      var tmp = d[2];
      d[2] = d[3];
      d[3] = tmp;
    }
    console.log(d);
    return Hangul.assemble(d);
    }).join('');
}

```

* input에 들어가는 텍스트 중에서 '관리' -> '고나리', '확인' -> '호가인', '훤하다' -> '허누하다'읭 방식으로 텍스트를 오타로 바꾸는 이벤트 핸들러 작성하기
*  https://github.com/e-/Hangul.js 에서 라이브러리를 받아서 자음과 모음을 분리하고, 다시 단어로 합치는 기능 살펴보기
* `String.split(' ') ` :  ` `` `  안에 있는 것에 기준으로 문자열을 잘라준다(return type: 배열)
* `Array.map(function(el){})` : 배열을 순회하면서 하나의 요소마다 function을 실행시킴(el:순회하는 각 요소, return type: 새로운 배열)

1. textarea에 있는 내용물을 가지고 오는 코드
2. 버튼에 이벤트 리스너(click)를 달아주고, 핸들러에는 1번에서 작성한 코드를 넣는다.
3. 1번 코드의 결과물을 한글자씩 분해해서 배열로 만들어준다.
4. ㅍ
5. ㅍ
6. 결과물로 나온 배열을 문자열로 이어준다.(join)
7. 결과물을 출력해줄 요소를 찾는다.
8. 요소에 결과물을 출력한다.

```html
$.ajax({
	url: 어느 주소로 요청을 보낼지,
	method: 어떤 http method 요청을 보낼지,
	data: {
		k: v 어떤 값을 함께 보낼지,
	}
})
```





1,좋아요 버튼을 눌렀을 때

2.서버에 요청을 보낸다.(현재 유저와 현재 보고있는 이 영화가 좋다고 하는 요청)

3.서버가 할 일 

4.응답이 오면 좋아요 버튼의 텍스트를 좋아요 취소로 바꾸고, `btn-warning text-white`로 바꿔준다.

5.이미 좋아요가 눌렀을 경우