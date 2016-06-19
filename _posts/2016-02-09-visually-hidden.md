---
layout: post
date: 2016-02-09
title: "접근성을 지키며 텍스트를 숨기는 방법"
categories: css
author_name: jmaking
author_url: /author/jmaking
author_avatar: jmaking
show_avatar: false
read_time : 10
feature_image: feature-pineapple
show_related_posts: true
square_related: recommend-pineapple
published: false
---

# 접근성을 지키며 텍스트를 숨기는 방법

## 속성 이해

### `visibility: hidden;` and/or `display:none;`

이 스타일은 모든 사용자로부터 텍스트를 숨긴다. 콘텐츠가 스크린리더에 의해서 읽히길 원한다면 사용하지 마라. 하지만 읽히길 원하지 않다면 사용해라.

### `width: 0px;`, `height: 0px;` or other 0 pixel sizing techniques

```css
.element-invisible {
  height: 0;
  overflow: hidden;
  position: absolute;
}
```

스크린리더에서 읽히길 원한다면 컨텐츠의 사이즈를 0 픽셀로 하지마라. 컨텐츠에 적용된 `font-size:0;` 또는 `line-height:0;`가 가로공간이 존재할 지라도 스크린리더에서 작동하지 않을 수 있다. 이러한 기술들은 검색엔진에 패널티의 결과로 악의적으로 해석될 수 있다.

### `text-indent: -10000px;`

```css
.element-invisible {
  text-indent: -9999em;
  outline: 0;
}
```

이 스타일은 스크린리더에서 읽을 것이다. 하지만 form 또는 link 요소에 적용할 경우, 포커싱 되었을 때 위치를 정확히 표시할 수 없어 혼란을 준다.
또, RTL(Right to Left) 언어권에서 문제가 생긴다.

###  `position: absolute;` and Offscreen

```css
.element-invisible {
  position: absolute;
  top: -999999em;
  left: auto;
  width: 1px;
  height: 1px;
  overflow:hidden;
}
```

포커싱를 가지는 엘리먼트에 적용할 경우, 포커싱 되었을 때 엘리먼트로 이동이 화면을 보고있는 사용자들에게 불안함을 야기시킨다.

### CSS clip

```css
.element-invisible {
  position: absolute !important;
  clip: rect(1px 1px 1px 1px); /* IE6, IE7 */
  clip: rect(1px, 1px, 1px, 1px);
}
```

크롬, 사파리, 오페라에서는 스크린 가장자리에 엘리먼트가 있을 때 흥미로운 행동을 가진다. 만약 가로스크롤이 생기는 스크린보다 큰 엘리먼트는 잘렸을 때도(clipped) 스크롤이 생길 것이다.

### Positioned, Clipped, and (almost) Collapsed

```css
.element-invisible {
  position: absolute !important;
  height: 1px; 
  width: 1px; 
  overflow: hidden;
  clip: rect(1px 1px 1px 1px); /* IE6, IE7 */
  clip: rect(1px, 1px, 1px, 1px);
}
```
- 레이아웃에 영향을 끼치지 않도록 `position: absolute;`
- 스크린 리더가 읽을 수 있도록 `width: 1px; height: 1px;`
- 눈에 보이는 부분을 제거 `clip: rect(1px, 1px, 1px, 1px);`
- clip과 overflow의 차이점은 같은 박스를 대상으로 적용하지 않는다.
- clip은 content box에
- overflow는 border box(+padding)에

### [h5bp](https://github.com/h5bp/html5-boilerplate/blob/master/dist/doc/css.md#common-helpers)에서 사용하는 `.visuallyhidden`

```css
.visuallyhidden {
    border: 0;
    clip: rect(0 0 0 0);
    height: 1px;
    margin: -1px;
    overflow: hidden;
    padding: 0;
    position: absolute;
    width: 1px;
}
```

- 위처럼 safer를 추가하여 더욱 안전하게 사용한다.

## 궁금증
- `clip: rect(0 0 0 0);` VS `clip: rect(1px, 1px, 1px, 1px);`

## 참고
- [Invisible Content Just for Screen Reader Users - WebAIM](http://webaim.org/techniques/css/invisiblecontent/)
- [HIDING CONTENT FOR ACCESSIBILITY - By JONATHAN SNOOK](http://snook.ca/archives/html_and_css/hiding-content-for-accessibility)
- [Clip Your Hidden Content For Better Accessibility - By Thierry Koblentz ](https://developer.yahoo.com/blogs/ydn/clip-hidden-content-better-accessibility-53456.html)
- [Change screen-reader-text styles #1 - By GaryJones](https://github.com/RRWD/leiden/issues/1)

