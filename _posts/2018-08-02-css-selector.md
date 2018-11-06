---
layout: post
title: "CSS 선택자 모음"
excerpt: ""
categories: "css"
comments: false
published: false
---

## nth-last-child(n + x)
마지막 자식을 기준으로 선택

**마지막 자식에서부터 세번째 있는 아이**
자식이 a, b, c, d, e 라면 c 를 선택

```css
:nth-last-child(3)
```

**마지막 자식 세번째부터 첫번째 아이까지**
자식이 a, b, c, d, e 라면 a, b, c를 선택

```css
:nth-last-child(n+3)
```

## 참조(자세한 설명은 이곳에서)
- [Solved with CSS! Logical Styling Based on the Number of Given Elements](https://css-tricks.com/solved-with-css-logical-styling-based-on-the-number-of-given-elements/?utm_source=CSS-Weekly&utm_campaign=Issue-324&utm_medium=email#article-header-id-2)


