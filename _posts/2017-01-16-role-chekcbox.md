---
layout: post
title: "button role=\"checkbox\""
excerpt: "버튼을 체크박스로 만들기"
categories: [html]
comments: false
---

![드롭박스 캡쳐]({{site.url}}/{{site.baseurl}}img/post-assets/dropbox-checkbox.png)

## Checkbox

우연히 드롭박스에 파일을 올린 후 체크박스를 보고 코드를 확인하였다. button 으로 마크업하고, role 속성을 사용하여 checkbox로 의미부여를 하였다.

그냥 checkbox를 사용하면 굳이 role 속성을 주지 않아도 되지만, 체크박스 디자인을 변경할 때 input을 숨기고 추가적인 CSS를 사용하는 대신 이 방법도 괜찮은 것 같다.

하지만 자바스크립트로 aria-checked, checked(className)값을 토글시켜 줘야 한다.

선택 전

```html
<button role="checkbox" aria-checked="false" aria-label="행 선택" class="checkbox-button"></button>
```

선택 후

```html
<button role="checkbox" aria-checked="true" aria-label="행 선택" class="checkbox-button checked"></button>
```

## Table

리스트 마크업에 사용한 role의 사용도 기억하면 좋을 것 같아 기록한다.

```html
<table> => <ul role="presentation">
<tr> => <li role="row">
<th> => <div role="rowheader">
<td> => <div role="gridcell">
```

## 참고링크
- [접근성을 지키며 라디오버튼처럼 만들기](https://www.w3.org/TR/2016/WD-wai-aria-practices-1.1-20160317/examples/radio/radio.html)