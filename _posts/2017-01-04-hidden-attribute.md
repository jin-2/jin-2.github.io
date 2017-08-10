---
layout: post
title: "HTML attribute hidden"
excerpt: "hidden 속성을 사용하여 숨기기"
categories: [html]
comments: false
---

컨텐츠를 보이지 않게 할 때,
스크린리더에서 읽지 않아야 할 때,

저는 클래스 삽입하거나

```css
.hidden { display: none; }
```

자바스크립트로 인라인으로 CSS를 지정하거나

```javascript
var element = document.getElementById('content');
element.style.display = 'none';

// jQuery
$('#content').hide();
```

aria-hidden을 이용했었죠.

```css
[aria-hidden="true"] { display: none; }
```

## 방법 하나 더, hidden 속성을 이용하는 것! (**IE11부터 지원가능**)

```html
<div hidden>I am not hidden</div>
<div hidden aria-hidden="true">I am hidden</div>
```

**[W3C Code Example](https://www.w3.org/TR/html5/editing.html#the-hidden-attribute):**

```html
  <h1>The Example Game</h1>
  <section id="login">
  <h2>Login</h2>
  <form>
  ...
  <!-- calls login() once the user's credentials have been checked -->
  </form>
  <script>
  function login() {
  // switch screens
  document.getElementById('login').hidden = true;
  document.getElementById('game').hidden = false;
  }
  </script>
  </section>
  <section id="game" hidden>
  ...
  </section>
```
## `hidden` attribute, `display: none;` VS `aria-hidden`
[이 글](https://www.paciellogroup.com/blog/2016/01/the-state-of-hidden-content-support-in-2016/)의하면
hidden과 display:none은 컨텐츠 사용자에게 보여주지 않고,
aria-hidden은 스크린리더 사용자에게 보여주지 않는다.
그리하여 hidden과 aria-hidden을 같이 사용하는것을 권장하고 있다.

정확한 이유가 이해가 되지 않지만, 우선 권장하는 방법으로 사용해 봐야겠다.

## 참고링크
- [Writing HTML with accessibility in mind](https://medium.com/@matuzo/writing-html-with-accessibility-in-mind-a62026493412#.vb8xtwwpo)
- [The state of hidden content support in 2016](https://www.paciellogroup.com/blog/2016/01/the-state-of-hidden-content-support-in-2016/)
- [W3C - 7.1 The hidden attribute](https://www.w3.org/TR/html5/editing.html#the-hidden-attribute)
- [Clearboth - HTML5 명세](http://html5ref.clearboth.org/doku.php?id=html5:attribute:hidden)
- [Clearboth HTML5 명세 해석자료](http://html5.clearboth.org/editing.html#the-hidden-attribute)