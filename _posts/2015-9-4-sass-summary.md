---
layout: post
title:  "Sass 요약 정리"
date:   2015-09-04 14:15:00
---

2015년 3월에 들었던 [야무](http://yamoo9.net/)쌤의 Sass 수업내용을 정리한다.

> ‘CSS를 확장한 언어’인 Sass는 CSS의 부족한 부분을 채워주는 강력한 도구입니다. 재사용 가능한 모듈을 활용해서 생산성을 높이고 편리하게 유지보수할 수 있습니다. 압축된 스타일 형식으로 출력파일을 만들어서 웹사이트의 성능을 최적화할 수 있습니다. 
> 야무(지훈)

**Sass, Less, Stylus 중에서 Sass를 사용하는 이유는?**  
 - Sass > Less > Stylus 순으로 점점 단순해지는 과정으로 국내 사용자에게 점점 더 이해하기 어렵다. (특히 Stylus)  
- 역사가 탄탄하다.  
- 버전관리가 잘된다.  

**Sass가 왜 생겼을까?**  
 - CSS는 단순 반복 > 언어의 변화 > 스크립팅 > 자바스크립트 접목 > 벤더프리픽스… 등 체크해야 할 것이 많아짐 > 기계가 해결해야 함

**Ruby Sass or Node Sass**  
 - 처리속도는 Node Sass가 더빠르다.  
- 기능 면에서는 Ruby Sass가 더 다양하다.  

###Ruby Sass Install-Window  
*Ruby와 Sass를 설치**  
[Ruby 설치(환경설정](http://rubyinstaller.org/downloads/)  
 - 32bit, 64bit 확인  
- 설치 중 □ add ruby executables to your PATH 체크  

[Git bash 설치(선택사항)](http://git-scm.com/)  
 - simmple context menu 체크(우클릭 메뉴추가 할 때)  
- use git from the windows command ( bash 이외에 커맨드 창 쓸거면 체크)  

###Sass cmd에서 설치하기  
{% highlight ruby %}
Install sass
gem install sass

#=>Double-check(sass 버전확인 및 설치확인)
sass -v
{% endhighlight %}

###Sass파일을 CSS파일로 변환하는 과정 → Preprocessing  
**한개의 파일만 변환  
{% highlight ruby %}
sass input.sass output.sass
{% endhighlight %}

**여러개 파일이 있는 폴더 변환(sass 폴더 내부의 파일을 css 폴더 내부에 변환/저장)  
{% highlight ruby %}
sass --watch sass:css
{% endhighlight %}

**Window에서 sass파일에 한글 에러가 날 때  
{% highlight ruby %}
sass -watch -E UTF-8 sass:css
{% endhighlight %}

**sass폴더에서 css폴더로 변경사항을 관찰하면서 compressed(nested, expanded, compact, compressed-출력스타일 종류)파일로 변환.  
{% highlight ruby %}
sass --watch -E UTF-8 -t compressed sass:css
{% endhighlight %}

**SCSS ↔ SASS 파일 변환  
[http://www.sasstoscss.com](http://www.sasstoscss.com)  
[http://css2sass.herokuapp.com](http://css2sass.herokuapp.com)  
{% highlight ruby %}
sass-convert style.scss style.sass
{% endhighlight %}
변환종료 **ctrl + c

SASS 작성법
syntax
SCSS: CSS 문법과 유사하므로 친숙함
.sytax{
    margin: 0 auto;
    padding-bottom: 20px/5;
}

SASS: {}, ; 등을 사용하지 않는 대신 들여쓰기가 매우 중요
.sytax
    margin: 0 auto
    padding-bottom: 20px/5


주석
/*
* 여러 줄 주석의 경우는
* CSS 컴파일 되어도 주석이 남아 있습니다.
*/

// 한 줄 주석의 경우는 CSS에서 지원하지 않기 때문에 
// CSS 컴파일 시, 주석이 표시되지 않습니다.

중첩규칙
쓸데없는 CSS 선택자를 남용하지 않고, 적당히 중첩하는게 중요하다.
	CSS
#page .container .section{
    margin: 1em 0;
}

SASS
#page 
    .container 
        .section
            margin: 1em 0



부모, 참조 선택자(&)
앤퍼센트(&) 심볼은 부모를 참조하는 선택자 역할을 수행합니다.
sass
.radius
    border-radius: 5px
    .ie8 &
        position: relative
        @extend %pie

css
.radius{
    border-radius: 5px;
}
.ie8 .radius{
    position: relative;
    behavior: url(/js/front/vendor/PIE.htc);
}

선택자 상속(Selector Inheritance)
@extend를 사용해 선언된 다른 규칙의 내용을 상속할 수 있습니다.(그룹핑됨)
%button 
    padding: 7px 20px
    background-color: $color-main

.button-checkout 
    @extend %button
    background-color: darken($color-main, 20%)



선택자 상속, 옵션(!optional) 설정
@extend  상속 시, 선언된 선택자가 존재하지 않을 경우 ‘옵션’ 처리하여 오류를 발생시키지 않습니다.

대체 선택자(Placeholder Selector, %)
Sass는 특수한 선택자 ‘%대체 선택자’를 지원합니다. 해석된 CSS에서는 출력 되지 않습니다.
// 말줄임
%ellipsis
    overflow: hidden
    text-overflow: ellipsis
    white-space: nowrap

// PIE.htc
%pie
    behavior: url(/momHTML2/public/js/front/vendor/PIE.htc)

// image sprite 
%is
    background: url(../img/bg_collect.png) no-repeat 0 0


호출
Scss, Sass 확장자의 경우는 생략할 수 있습니다.
여러 개의 파일을 불러들일 때는 콤마로 구분하여 불러들일 수 있습니다.

@import “placeholder”, “grid”

_호출 제어(Partials)
기본적으로 Scss, Sass 파일은 해석되어 CSS로 변경됩니다.
Scss, Sass 파일 앞에 언더바(_)가 붙어 있으면 이를 CSS로 해석 변경하지 않습니다.

@import modules/normalize
@import modules/base
@import modules/mixins
@import partials/header
@import partials/footer
@import partials/ie
@import partials/print

SASS Script
변수(Variables, $)
PHP 변수처럼 $ 이름 값을 설정한 후, 값을 참조하여 적용할 수 있습니다.
- , _ 구분하지 않고 같은 데이터로 인식함.
속성(Property)도 변수 처리가 가능.
변수에 연산 수행
$background-color: #eee
#container
    background-color: $background-color

$width-name: max-device-width
$break-small: 320px
$break-large: 1200px
#content
    {padding: 0 50px}
    @media screen and ($width-name: $break-small)
        {padding: 0 5px}
    @media screen and (min-width: $break-large + 1)
        {padding: 0 100px}

변수 기본 값 설정($, !default)
변수를 설정한 후, 초기 값을 지정할 수 있습니다.
$point-color: #e0e0e0
$point-color: #EB3B4B !default
.note
    color: $point-color // #e0e0e0


데이터 유형 - 6가지
Sass는 6가지 데이터 형을 지원합니다.
Numbers 
숫자형
1.2, 3, 14px
Nulls 
비어있음
Strings & Colors 
문자형
“../images/thumb.jpg” | “Times New Roman” |  Verdana | lightblue | #123456
Booleans 
논리형(참, 거짓)
true, false
Lists 
공백, 콤마(,)로 구분되는 목록 (Javascript 배열과 유사), 관련 함수
1em 2em 3em 4em | 1px solid red | Helvetica, Sans-Serif
Maps 
키:값 으로 구성된 그룹 (Javascript 객체와 유사), 관련 함수로 값을 얻을 수 있습니다.
	$map: (key1: value1, key2: value2)

연산(Operations)
덧셈(+), 뺄셈(-), 곱셈(*), 나눗셈(/), 나머지(%) 등 수학의 연산 결과를 수행할 수 있습니다.
width: 10px
$double_width: $width * 2   // 10 × 2 = 20px
$half_width: $width / 2     // 10 ÷ 2 = 5px
$width_plus_2: $width + 2   // 10 + 2 = 12px
$width_minus_2: $width - 2  // 10 -2 = 8px

$base: 13px
body
    font: $base / 1.5 Dotum
    $base: 13
    font: $base+px / 1.5 Dotum
▼ compile
body{
    font: 8.66667px Dotum;
    font: 13px/1.5 Dotum
}

p {
  color: #010203 * 2;
}
/*
01 * 2 = 02
02 * 2 = 04
03 * 2 = 06
------------
#020406
*/


비교연산(Comparison Operations)
크다(>), 작다(<), 크거나 같다(>=), 작거나 같다(<=), 같다(==), 다르다(!-) 등 비교 연산 결과를 제공합니다.

문자연산(String Operationsf)
문자와 문자를 접합하려는 경우 + 연산자를 사용할 수 있습니다.
Javascript와 달리 “”, ‘’를 붙이지 않아도 연산이 수행됩니다.

보간법(#{}, Interpolation)
Sass는 변수를 “”내부에서 처리할 수 잇는 보간법을 지원합니다.
$family: unquote("Droid+Sans");
@import url("http://fonts.googleapis.com/css?family=#{$family}");


Mixins
믹스인(@mixin)
JS 함수와 흡사한 믹스인은 @mixin으로 모듈을 정의한 후, @include로 호출할 수 있어 재사용이 가능합니다.
@mixin box-shadow($shadows...) {
  -moz-box-shadow: $shadows;
  -webkit-box-shadow: $shadows;
  box-shadow: $shadows;
}

.shadows {
  @include box-shadow(0px 4px 5px #666, 2px 6px 10px #999);
}

▼compile
.shadows {
  -moz-box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
  -webkit-box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
  box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
}

전달 인자(Arguments)
JS 함수 확장처럼 @mixin으로 정의된 모듈에 인자를 전달하여 믹스인을 확장할 수 있습니다.
$shadows 는 일종의 변수로 믹스인 내부에 전달된 값을 받기에 전달인자라고 부릅니다.

전달 인자 기본 값 설정(Args, Default Value)
믹스인 호출시 값을 전달하지 않아 오류가 발생하는 것을 방지하기 위해 특정 값을 기본으로 설정할 수 있습니다. 오류를 방지함.
@mixin border-radius( $radius: 4px ){
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    border-radius: $radius;
}

.box{
    @include border-radius; //4px 대입
}

.box-round{
    @include border-radius(50%);
}

변수 범위(Scope)와 콘텐츠 블록(@content)
변수 범위는 JS의 전역/지역 변수 개념과 유사하며, 콘텐츠 블록은 믹스인 호출 시 {} 코드문입니다.

믹스인 *.sass 문법
@mixin은 “=”으로, @include는 “+”로 선언/호출이 가능합니다.

function
컬러 함수 (Color Functions)
RGBA 함수
rgb($red, $green, $blue)
rgba($red, $green, $blue, $alpha)
rgba($color, $alpha)

HSLA 함수
hsl($hue, $saturation, $lightness)
hsla($hue, $saturation, $lightness, $alpha)

lighten($color, $amount)
darken($color, $amount)
saturate($color, $amount)
desaturate($color, $amount)
grayscale($color)
complement($color) // 보완색
invert($color) // 반전색

Opacity 함수
// SET 함수
rgba($color, $alpha)
// 불투명하게 변경 함수, $amount 값은 0~1 사이 소수
opacify($color, $amount) / fade-in($color, $amount)
// 투명하게 변경 함수, $amount 값은 0~1 사이 소수
transparentize($color, $amount) / fade-out($color, $amount)

수학 함수 (Number Functions)
Number 함수
	퍼센트 변경 함수
percentage(13/25) // 52%


반올림 함수
round(2.4) // 2

올림 함수
ceil(2.2) // 3

내림 함수
floor(2.6) // 2

절대값 함수
abs(-24) // 24

비교하여 작은것을 반환하는 함수
min(10px/12px) // 10px

비교하여 큰것을 반환하는 함수
max(10px/12px) // 12px

난수 함수
random(1) // 0~1

사용자 정의 함수(@function)
JS 함수와 거의 흡사한 함수로 @function으로 모듈을 정의한 후, 이름으로 호출할 수 있어 재사용이 가능합니다.
$grid-width: 40px;
$gutter-width: 10px;

@function grid-width($n) {
    @return $n * $grid-width + ($n - 1) * $gutter-width;
}

#sidebar { width: grid-width(5); } // 5 * 40 + (5-1) * 10 = 240px

add-on
sass-globbing
세분화된 각각의 모듈을 Sass 코드로 불러오려면 다수의 @import 문이 필요합니다.
sass-globbing 애드온을 설치하면 하나의 @import 문으로 다수의 Sass 파일을 호출할 수 있습니다.

# 명령어 프롬프트 툴(Terminals, CMD)에서 gem을 통해 install 합니다.
sudo gem install sass-globbing
# 명령어 프롬프트 툴(Terminals, CMD)에서 sass 명령어를 입력하여 수행하려 watch 합니다.
sass -r sass-globbing --watch sass_dir:css_dir
# 폴더 내부에 존재하는 모든 Sass 파일을 호출합니다. (서브 폴더 제외)
@import “library/mixins/*”
# 폴대 내부에 존재하는 모든 Sass 파일을 호출합니다. (서브 폴더 포함)
@import “library/**/*”


	