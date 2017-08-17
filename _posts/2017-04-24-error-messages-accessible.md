---
layout: post
title: "접근성있게 에러 메시지를 만드는 방법"
excerpt: "잡을 만들고 소스 체크아웃까지"
categories: [html]
comments: false
---

원문: [How to make error messages accessible](https://hiddedevries.nl/en/blog/2017-04-04-how-to-make-error-messages-accessible)

[여기](http://seminar1505.publisher.name/#/6/3) 잘 정리된 한글 문서가 있다.

``` html
<ul aria-live="polite" aria-relevant="all" aria-atomic="false">
<li>...</li>
<li>...</li>
<li>...</li>
</ul>
```

그리고 아래는 WAI-ARIA 책에서 발췌한 내용이다.
에러가 발생한 `input` 요소에 aria-invalid="true" 정의하고,
폼의 에러 메시지 id="", `input` aria-describedby="" 값을 연결하여 준다.

달력과 같이 특정 폼과 연결할 수 없는 에러가 발생할 때
스크린리더와 호환될 수 있는 방법은 role="alert"과 aria-live="assertive" 삽입한다.

role="alert"는 스크린리더가 읽더 내용을 끊고 동적으로 삽입된 내용을 읽게 되므로 주의해서 사용해야 한다.

``` html
<!-- 폼과 연결된 에러 -->
<div>
  <label for=“fname”>성 <span aria-hidden=“true”>*</span>
  <span class=“offscreen”>필수입력항목</span></label>
  <input type=“text” id=“fname” aria-invalid=“true” aria-describedby=“error-text”>
  <div class=“error” id=“error-text”>성을 입력하여 주세요.</div>
</div>
<button class=“btn”>Confirm</button>
<!-- 폼과 연결되지 않는 에러 -->
<div class=“error” id=“error-text” role=“alert” aria-live=“assertive”>
  <span>성 입력 오류</span>
</div>
<button class=“btn”>Confirm</button>
```