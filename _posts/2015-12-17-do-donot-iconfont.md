---
layout: post
date: 2015-12-17
title: "아이콘폰트를 써야할까 말아야할까"
categories: css
author_name: jmaking
author_url: /author/jmaking
author_avatar: jmaking
show_avatar: false
read_time : 10
feature_image: feature-pineapple
show_related_posts: true
square_related: recommend-pineapple
---

메일로 받아보는 CSS Weekly 글 중 "Seriously, don't use Icon Fonts" 글을 읽었다. 그리고 다음 메일에 "Seriously, use Icon Fonts"를 읽었다. 아이콘 폰트를 편리하게만 사용했었는데 이런 깊은 내용들이 WOW~ 나중에 댓글도 읽어봐야겠다. 아주 의견들이 많다.

---

영어는 잘 못하지만 짧게 요약한 내용이다.

### [Seriously, Don’t Use Icon Fonts](http://blog.cloudfour.com/seriously-dont-use-icon-fonts/?utm_source=CSS-Weekly&utm_campaign=Issue-190&utm_medium=email)
- **스크린리더에서 의도치않게 아이콘폰트를 읽게된다.**('favarite'아이콘은 'black favarite star'로 읽게 된다.)
난독증을 가진 사람들은 OpenDyslexic같은 오픈소스의 도움을 받는데 여기서 아이콘폰트의 변환을 하지못하여 깨지게 보인다.
- **유니코드는 자동 선택기로 변환이 되는데 모바일이나 다른 브라우저에서 다른 이모티콘으로 겹쳐질 수 있다.**
종종 아이콘폰트가 로드에 실패되면 이상한 모양으로 나타난다. 부트스트랩에서도 다음버전에 아이콘폰트를 제외시켰다.
- **font-smooth가 브라우저에 전부 지원되지 않아 아이콘폰트는 깨져 보일 수** 있고, 컬러풀한 아이콘은 프린트됬을 때 정확하게 색상구현이 안된다.
- font-face가 지원되지 않는 환경, 어떠한 이유로 **아이콘이 로드되지 않는 환경** 등... 아이콘 폰트는 신중하게 사용하여야 한다.
- [확실한 아이콘 폰트 사용법](https://www.filamentgroup.com/lab/bulletproof_icon_fonts.html)

#### 더 좋은 방법 SVG
- SVG는 스프라이트로 결합할 수 있다.
- Gzip과 SVG최적화로 크기를 줄일 수 있다.
- 마크업은 길지만, 비어있는 span보다 마크업되어 더욱 시맨틱하여 접근성에 좋다.
- SVG에 대한 지원은 증가하고 있고, 대비책도 간단하다.
- 프레임워크에서 아이콘폰트를 지원하지 않을 수 있다.

---

### [Seriously, use icon fonts](http://benfrain.com/seriously-use-icon-fonts/?utm_source=CSS-Weekly&utm_campaign=Issue-192&utm_medium=email)
아이콘 폰트를 써야만 한다는 게 아니라, 어떤 문제에 대해 아이콘 폰트는 좋은 해결책이 될 수 있다는 생각.

- **Need to support Android 2.3?**: 오래된 브라우저를 위해 SVG를 PNG 폴백과 함께 제공하여야 한다. 대부분 아이콘들은 다양한 색과 애니메이션도 없다. 예를 들어 화살표, 쇼핑카트 아이콘, 리프레쉬 아이콘 등. 아이콘 폰트는 색깔과 크기들을 쉽게 바꿀 수 있다. 
- **You don’t need multiple font formats**: IE를 제외하면 [TTF 포맷](http://caniuse.com/#search=ttf)으로 모든 브라우저에서 볼 수 있다. CSS에  data URI를 삽입하면 아이콘 폰트가 로딩에 실패하는 일을 없을 것이다.
- **Icon fonts make it simple to work with designs**: 디자인에 적합한 [아이콘](https://icomoon.io/docs.html)을 붙여넣고, CSS로 폰트사이즈를 수정하여 크기도 쉽게 바꿀 수 있다. SVG는 IE를 지원하기 위한 [shim script](https://github.com/jonathantneal/svg4everybody)가 필요하다.
- **PUA and accessibility**: 아이콘 폰트는 비주얼적인 부분을 향상시키기 위해 사용하고, 인터페이스에서 중요하게 사용하진 않는다. 스크린 리더에서는 PUA는 읽지 않는다. The private use area of Unicode is expressly for custom glyphs. Icon fonts are custom glyphs.(Icon font = PUA)
- **Bonus points for Icon Fonts**: CSS만으로 text shadows, transition colours, perfect alignment, surrounding text 꾸밀 수 있다.(?)
- **Pages render faster with icon fonts**: [연구결과](http://blog.nparashuram.com/2015/05/icons-font-inline-svg-or-background-svgs.html#svg-perf-test-results)가 있다. Result: *Font Icons > Background SVG > Inline SVG* 브라우저가 업데이트되고 기술이 향상되어 이 결과값 또한 변화할 수 있지만, 아직 여기에 대응되는 자료가 없다. 속도가 중요하다면 SVG보다 아이콘 폰트가 더 나은 선택이다.
- **summary**: 기술에 대한 장단점을 알고 상황에 맞게 사용하는게 최선의 방법이다.

---

### Note
**PUA(Private Use Area)**
In Unicode, a Private Use Area (PUA) is a range of code points that, by definition, will not be assigned characters by the Unicode Consortium. 유니 코드, 개인 사용 영역 (PUA)을 정의함으로써, 유니 코드 컨소시엄에 의해 문자가 할당되지 않으며 코드 포인트의 범위이다.

*잘못된 내용은 메일로 보내주시면 정말 감사감사합니다.*