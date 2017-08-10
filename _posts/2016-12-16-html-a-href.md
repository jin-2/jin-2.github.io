---
layout: post
title: "a 태그에 링크를 사용하지 않을 때"
excerpt: "자료 정리"
categories: [html]
comments: false
---

유지보수를 하면서, a 태그 링크 이동을 사용하지 않을 때가 있다. 우리가 한번쯤은 보았을 아래와 같은 코드들로 링크의 기능을 사용하지 않지만, [이 블로그](http://wit.nts-corp.com/2014/04/14/1297)의 글처럼 role="button" 속성을 사용하여 버튼을 명시해주거나, 목적에 맞게 button 태그를 사용하여 바꾸어 주자.

## 우리가 봤을 코드들

### void(0)

```html
<a href="javascript:void(0);">링크없는 요소</a>
```

```javascript
void(0) // undefined
```

해당하는 링크가 정상적으로 동작하지 않게 만들기 위하여 이처럼 `void(0)`를 사용한다.

### href="#"

```html
 <a href="#">링크없는 요소</a>
```

링크 이동을 하지 않지만 url 최상단인 페이지로 이동한다.

### href="#none"

```html
 <a href="#none">링크없는 요소</a>
```

id 값이 없는 name을 작성해 주면 화면 이동을 하지 않는다.(이동할 곳이 없다.)

### href="javascript:;"

```html
<a href="javascript:;">링크없는 요소</a>
```

### onclick="return false;"

``` html
<a href="#" onclick="return false;">링크없는 요소</a>
```

### event.preventDefault();

```javascript
$('a[href="#"]').click(function(event) {
  event.preventDefault();
 })
```

`prevendDefault()`는 `href`로 연결해 주지 않고 단순히 click에 대한 처리를 하도록 해준다.

## 참고링크

- [**HTML의 원래 기능을 유지하자. - a 태그부분**](http://wit.nts-corp.com/2014/04/14/1297)
- [href 속성에 javascript void:(0) 사용하는 이유](http://webisfree.com/blog/?titlequery=href-%EC%86%8D%EC%84%B1%EC%97%90-javascript-void:-0-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0)
- [앵커링크 이동 막기](http://shinyssun.tistory.com/entry/%EC%95%B5%EC%BB%A4%EB%A7%81%ED%81%AC-%EC%9D%B4%EB%8F%99-%EB%A7%89%EA%B8%B0)
- [event.stopPropagation(), event.preventDefault () 이해하기](http://ismydream.tistory.com/98)
- [a href="#" 일 경우 페이지 최상단으로 이동하는 것 막기](http://www.seobangnim.com/zbxe/111591)
