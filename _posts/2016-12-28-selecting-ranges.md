---
layout: post
title: "CSS 셀렉터를 이용하여 범위를 선택"
excerpt: "code"
categories: [css]
comments: false
---

> “select the 7th element, then every element after that.”

```css
ol li:nth-child(n+7):nth-child(-n+14) {
  background: lightpink;
}
```

## Safari fixed bug

> “select the 14th element, and every element before that.”

```
ol li:nth-child(-n+14):nth-child(n+7) {
  background: lightpink;
}
```

## 원문
[12 Little-Known CSS Facts (The Sequel)](https://www.sitepoint.com/12-little-known-css-facts-the-sequel/?utm_source=frontendfocus&utm_medium=email)