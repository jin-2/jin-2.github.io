---
layout: post
title: "clearfix 핵 없이 clearing하는 법"
excerpt: "display: flow-root;"
categories: [css]
comments: false
---

[이 글](https://rachelandrew.co.uk/archives/2017/01/24/the-end-of-the-clearfix-hack/?utm_source=frontendfocus&utm_medium=email)을 통해서
앞으로 [clearfix 핵](http://cssmojo.com/the-very-latest-clearfix-reloaded/)없이 clearing 할 수 있는 속성을 알게 되었다.
아직은 chrome canary와 firefox Nightly에서 확인 가능하다.

아래 코드처럼 사용하면 된다.

```css
.container {
  display: flow-root;
}
```

그리고 유용한 덧글내용 중,
`@support` 를 사용한 코드를 제시했는데 유용하게 사용할 수 있을 것 같다.
[@support 는 익스플로러와 안드로이드 브라우저에서 지원이 안된다.](http://caniuse.com/#search=%40support)

```css
.clearfix: after {
  content: “”;
  display: block;
  clear: both;
}

@supports (display: flow - root) {
.clearfix {
display: flow - root;
}
.clearfix: after {
display: none;
}
}
```
