---
layout: post
title: "책요약 - JavaScript for Web Developers 7"
excerpt: "참조타입(Date, RegExp) 내용 정리"
categories: [js]
comments: false
---

## 5장 참조 타입

### 5.3 Date 타입
Date 타입은 날짜와 시간을 저장할 때 1970년 1월 1일 자정부터 몇 밀리초가 지났는지 나타내는 숫자를 사용합니다.

```javascript
var now = new Date(); // Mon Nov 02 2015 14:47:22 GMT+0900 (KST)
```

1970년 1월 1일 자정으로부터 몇 밀리초가 지났는지 나타내는 숫자를 매개변수로 넘겨야 합니다. 이 계산은 복잡하고 실수하기 쉬우므로 ECMAScript에는 이를 처리하는 메서드 `Date.parse()`와 `Date.UTC()`가 있습니다.

##### Date.parse()
매개변수로 날짜를 표현하는 문자열을 받고 해당 문자열을 날짜의 밀리초 표현으로 변환을 시도합니다.

```javascript
// 결과가 같다.
var someday = new Date(Date.parse("may 25, 2004"));
var someday = new Date("may 25, 2004");
```

##### Date.UTC()
매개변수는 해당 시각의 년, 월 인덱스(0이 1월), 일(1~31), 시(0~23), 분, 초, 밀리초입니다. 이들 중 필수 매개변수는 첫 번째와 두 번째(년, 월 인덱스) 뿐입니다. 일을 생략하면 1일로 간주하며 다른 매개변수는 모두 0으로 간주합니다.

```javascript
var y2k = new Date(Date.UTC(2000, 0));
var allFives = new Date(Date.UTC(2005, 4, 5, 17, 55, 55));
console.log(y2k); // Sat Jan 01 2000 09:00:00 GMT+0900 (KST)
console.log(allFives); // Fri May 06 2005 02:55:55 GMT+0900 (KST)

// 차이점: 날짜와 시간을 GMT가 아니라 지역 시간을 사용합니다.
var y2kOther = new Date(2000, 0);
```
    
GMT
:	Greenwich Mean Time(그리니치 평균시)의 약자이며, 우리나라는 GMT+9입니다.

UTC
:	Coordinated Univeral Time(협정 세계시)의 약자인데 GMT와 UTC는 초의 소수점 단위에서만 차이가 나기 때문에 같다고 봐도 무방하며 실제로 많이 혼용됩니다.

#### now()
ECMAScirpt5에 추가, 현재 시각을 밀리초 표현으로 반환합니다. 이 메서드를 쓰면 코드의 실행 시간을 측정하는 프로파일링 작업을 다음과 같이 쉽게 할 수 있습니다.

```javascript
// 시작 시간
var start = Date.now(); // 1446443236221

// 실행 시간을 잴 함수
doSomething();

// 끝난 시간
var stop = Date.now(),
    result = stop - start;
```        

Data.now() 메서드를 지원하지 않는 브라우저에서는 + 연산자를 써서 Date 객체를 숫자로 전환하여 같은 방법으로 활용할 수 있습니다
```javascript
// Date.now() 대체 방법

var start = +new Date();

doSomething();

var stop = +new Date(),
    result = stop - start;
```

! Browser Supported
:	인터넷 익스플로러 9 이상, 파이어폭스 3 이상, 사파리 3 이상, 오페라 10.5이상, 크롬

#### 5.3.1 상속된 메서드
toLocaleString(), toString(), valueOf() 메서드를 오버라이드 합니다.

##### toLocaleString()
날짜와 시간 형식을 브라우저가 실행 중인 지역의 관습에 맞게 바꿔서 반환합니다.

##### toString()
일반적으로 날짜와 시간에 타임존 정보를 포함하며 시간은 24시간 형식으로 표시합니다.

**! note**
브라우저마다 출력 형식이 다르므로 toLocaleString()이나 toString()는 사실 디버그 목적으로나 쓸만하지 사용자에게 표시하기에는 적당하지 않습니다.

##### valueOf()
이 메서드가 반환하는 값은 문자열이 전혀 들어있지 않습니다. 비교연산자( `<`, `>`)가 정확히 작동하도록 밀리초 표현을 쓰기 때문입니다.

#### 5.3.2 날짜 표시 메서드
Date 타입에는 날짜를 특정한 형식으로 표현하는 메서드가 여럿 있습니다.

- toDateString()
- toTimeString()
- toLocaleDateString()
- toLocaleTimeString()
- toUTCString()
(정확한 형식은 브라우저에 따라 다릅니다.)

#### 5.3.3 날짜/시간 부속 메서드
p.158~159

### 5.4 RegExp 타입
ECMAScript는 RegExp 타입을 통해 정규 표현식을 지원합니다.

```javascript
var expression = /pattern/flags;
```

#### 각 정규 표현식은 플래그(flag)를 통해 해당 정규 표현식이 어떻게 동작할지 나타냅니다.
플래그에는 세 가지가 있습니다.

1. `g`  
전역 모드를 지정합니다. 이 플래그를 지정하면 문자열에서 패턴을 찾는 즉시 종료하지 않고 문자열 전체에서 동작합니다.

2. `i`  
대소문자 비구분 모드를 지정합니다. 이 플래그를 지정하면 패턴을 찾을 때 대소문자를 구분하지 않습니다.

3. `m`  
여러 줄 모드를 지정합니다 이 플래그를 지정하면 텍스트의 줄 끝에 도달해도 멈추지 않고 계속 패턴을 찾습니다.

#### '메타 문자'를 패턴에 쓸 때는 반드시 이스케이프해야 합니다.

```
( [ { \ ^ $ | ) ] } ? * + .
```

#### Sample Code - 정규 표현식 리터럴을 사용

모든 "at"에 일치
```javascript
var pattern1 = /at/g;
```

"bat"나 "cat" 중 처음 나온 것에 일치, 대소문자 구분 없음
```javascript
var pattern2 = /[bc]at/i;
```

처음 나온 "[bc]at"에 일치, 대소문자 구분 없음
```javascript
var pattern2 = /\[bc\]at/i;
```

"at"으로 끝나는 세 글자에 모두 일치, 대소문자 구분 없음(. 문자는 "at"앞에 무슨 글자가 있든 상관없다는 뜻)
```javascript
var pattern3 = /.at/gi;
```

".at"에 모두 일치, 대소문자 구분 없음
```javascript
var pattern3 = /\.at/gi;
```

#### RegExp 생성자를 사용
매개변수를 두 개 받는데 하나는 패턴이 될 문자열이며 옵션인 두 번째 매개변수는 플래그를 나타내는 문자열입니다

```javascirpt
var pattern2 = new RegExp("[bc]at", i);
```

##### RegExp 생성자에 메타 문자를 쓸 때는 반드시 이중으로 이스케이프해야 합니다.
왜냐하면 RegExp 생성자의 패턴 매개변수에 문자열을 쓰기 때문입니다.

| 리터럴 패턴      | 문자열                |
|------------------|-----------------------|
| /\[bc\]at/       | "\\[bc\\]at"          |
| /\.at/           | "\\.at"               |
| /name\/age/      | "name\\/age"          |
| /\d.\d{1,2}/     | "\\d.\\d{1,2}"        |
| /\w\\hello\\123/ | "\\w\\\\hello\\\\123" |

#### 5.4.1 정규 표현식 인스턴스 프로퍼티
RegExp 인스턴스에는 다음 프로퍼티가 있으며 각 프로퍼티는 패턴에 대한 정보를 포함합니다.
일반적으로 많이 쓰이지 않는데, 패턴 선언을 선언할 때 명시하는 플래그이므로 개발자가 이미 알고 있는 것이기 때문입니다.

```javascript
var pattern1 = /\[bc\]at/i;

pattern1.global
pattern1.ignoreCase
pattern1.mutiline
pattern1.lastIndex
pattern1.source
```

#### 5.4.2 정규 표현식 인스턴스 메서드

##### exec()
이 메서드는 패턴을 테스트할 문자열을 매개변수로 받고 패턴에 일치하는 문자열 배열을 반환하며 일치하는 부을 찾을 수 없을 때는 null을 반환합니다.

`exec()` 메서드가 반환하는 배열은 Array의 인스턴스인 동시에 프로퍼티 두 개가 추가됩니다.
- index 프로퍼티는 패턴이 일치한 위치를 나타내며,
- input 프로퍼티는 exec() 메서드에 넘긴 문자열입니다.

```javascript
var text = "cat, bat, sat, fat";
var pattern1 = /.at/;

var matches = pattern1.exec(text);
console.log(matches.index);     // 0
console.log(matches.input);     // "cat, bat, sat, fat"
console.log(matches[0]);        // cat
console.log(matches.lastIndex); // 0

// 패턴에 g 플래그가 설정되어 있으면 exec()를 호출할 때마다
// 문자열 안쪽으로 더 깊숙이 들어가며 검색하여 다음과 같은 결과를 반환합니다.
var pattern2 = /.at/g;

var matches = pattern1.exec(text);
console.log(matches.index);     // 0
console.log(matches[0]);        // cat
console.log(matches.lastIndex); // 3

var matches = pattern1.exec(text);
console.log(matches.index);     // 5
console.log(matches[0]);        // bat
console.log(matches.lastIndex); // 8
```

##### test()
이 메서드 역시 문자열을 매개변수로 받지만 반환 값이 달라서,
문자열이 패턴에 일치할 때는 true를 반환하고 그렇지 않을 때는 false를 반환합니다.
이 메서드는 **문자열이 패턴에 일치하는지만 확인**하면 되고
실제로 어떤 문자열이 일치하는지는 알 필요가 없을 때 유용합니다.

```javascript
var text = "000-00-0000";
var pattern = /\d{3}-\d{2}-\d{4}/;

if (pattern.text(text)) {
    alert("The pattern was matched.");
}
```
*\d : 숫자, [0-9]와 같음*

#### 5.4.3 RegExp 생성자 프로퍼티
이들 프로퍼티의 또 다른 특징은 두 가지 방법으로 접근할 수 있다는 점입니다. 각 프로퍼티에는 정식 이름과 짧은 이름이 있는데 오페라는 짧은 이름을 지원하지 않습니다.

정규 표현식 생성자에는 캡처 그룹을 아홉 개까지 저장할 수 있는 프로퍼티도 있습니다.

```
var text = "this has been a short summer";
var pattern = /(..)or(.)/g;

if (pattern.test(text)) {
    console.log(RegExp.$1); // sh
    console.log(RegExp.$2); // t
}
```

#### 5.4.4 패턴의 한계
다음 기능은 ECMAScipt 정규 표현식에서 지원하지 않는 기능입니다.

- 텍스트의 처음과 마지막에 일치하는 \A와 \Z
- 룩비하인드(룩어헤드의 반대 개념)
- 병합 클래스
- 최소 그룹(atomic group)
- 유니코드 지원(한 번에 한 문자를 찾는 기능은 지원합니다.)
- 이름 붙은 캡처 그룹
- s(한 줄 모드), x(공백 무시 모드) 플래그
- 조건문
- 정규 표현식 주석










