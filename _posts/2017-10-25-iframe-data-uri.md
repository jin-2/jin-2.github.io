---
layout: post
title: "iframe에서 Data URI로 컨텐츠 삽입"
excerpt: ""
categories: "html"
comments: false
---

[WebToolsWeekly](http://mailchi.mp/webtoolsweekly/web-tools-222?e=f32275ffc1) 내용 중 Data URI에 대해 몰랐던 내용을 기록한다.

[예제](https://jsbin.com/zovumu/edit?html,output)를 보면 Html과 스크립트를 적용할 수 있다.

```html
<iframe id="myFrame" src="data:text/html,<p>Click the background of this iframe to turn it gold.</p><script>document.addEventListener('click', function() { document.body.style.backgroundColor = 'gold'; }, false);</script>"></iframe>
```


