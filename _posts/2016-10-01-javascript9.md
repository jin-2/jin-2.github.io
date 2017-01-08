---
layout: post
title: "책요약 - JavaScript for Web Developers 9"
excerpt: "참조타입(원시 래퍼 타입) 내용 정리"
categories: [js]
comments: false
---

## 5장 참조 타입

### 5.6 원시 래퍼 타입
Boolean, Number, String은 원시 값을 편리하게 조작하기 위해 디자인된 참조 타입입니다.

```javascript
var s1 = "some test";
var s2 = s1.substring(2); // me test
```

원시 값은 객체가 아니므로 논리적으로는 메서드를 가질 수 없지만 별다른 코드 
없이도 메서드를 호출했고 정확히 동작했습니다.
두 번째 줄에서 읽기 모드로 s1에 접근하는 순간, 다시 말해 메모리에서 값을 읽는
순간 다음 세 단계가 일어납니다.

1. String 타입의 인스턴스를 만듭니다.
2. 해당 인스턴스에서 메서드를 호출합니다.
3. 인스턴스를 파괴합니다.

코드를 옮긴다면 다음과 같습니다.

```javascript
var s1 = new String("some text");
var s2 = s1.substring(2);
s1 = null;
```

이면에서 이런 동작이 발생하므로 원시 문자열 값을 마치 객체처럼 사용할 수 있습니다.
불리언과 숫자에서도 마찬가지로 Boolean과 Number 타입을 사용합니다.  
참조 타입과 원시 래퍼 타입의 **주요 차이는 그 생명 주기**입니다. new 연산자를 사용해
참조 타입의 인스턴스를 만들면 **스코프를 벗어날 때까지 메모리에 존재**하지만 자동으로
생성된 원시 래퍼 타입은 코드의 **해당 행을 벗어나는 즉시 파괴**됩니다. 따라서 원시 래퍼
타입에는 **런타임에** 프로퍼티나 메서드를 추가할 수 없습니다.

#### 원시값
'foo', true, false, null, undefined와 같은 자바스크립트 값은 **더이상 단순화**할 
수 없기 때문에 원시적(Primitive)이라 하며, 이러한 값을 가리켜 원시값이라 합니다. 

#### 래퍼 객체
래퍼(wrapper) 객체는 **원시(primitive) 타입의 값을 객체로 다루기 위한 객체**로 
number, string, boolean, symbol 데이터 타입에 각각 대응하는 Number, String, 
Boolean, Symbol이 제공된다.  
래퍼란 이름에서 드러나듯 래퍼 객체는 원시 타입의 값을 감싸는 형태로 생성된다. 

#### 참고링크
- [원시값](http://neeunbox.tistory.com/8)
- [래퍼 객체, Wrapper Objects](http://noritersand.tistory.com/536)

#### 5.6.1 불리언 타입
- Boolean 타입은 불리언 값에 대응하는 참조 타입입니다. 
- Boolean 객체를 생성하려면 다음과 같이 Boolean 생성자에 true나 false를 넘깁니다.  
- `valueOf()`, `toString()` 메서드를 오버라이드합니다.

```javascript
var booleanObject = new Boolean(true);
```

##### ECMAScript의 Boolean 객체에는 혼란스러운 점이 있어서 자주 쓰이지 않습니다.

```javascript
var falseObject = new Boolean(false);
var result = falseObject && true;
alert(result); // true

var fasleValue = false;
result = fasleValue && true;
alert(result); //false
```

불리언 표현식에서는 모든 객체를 자동으로 true로 변환하므로, **이 코드에서 falseObject
객체는 사실상 true 값과 마찬가지입니다.** 즉 이 표현식은 true && true를 평가한
것이므로 true입니다.(불리언 연산에서 false && true는 false입니다.)

원시 불리언 타입과 참조 불리언 타입 사이에는 아래 코드처럼 차이가 더 있습니다.

```javascript
console.log(typeof falseObject); // object
console.log(typeof falseValue); // boolean

console.log(falseObject instanceof Boolean); // true
console.log(falseValue instanceof Boolean); // boolean
```

**원시 불리언 값과 Boolean 객체를 반드시 구분할 수 있어야 하며 Boolean 객체는 
결코 쓰지 말기를 권합니다.**

#### 5.6.2 Number 타입
- Number 타입은 숫자형 값의 참조 타입입니다.
- `valueOf()`, `toLocaleString()`, `toString()` 메서드를 오버라이드 합니다.

```javscript
var numberObject = new Number(10);
```

##### toString()
- 문자열 반환
- 옵션으로 진법 매개변수를 받습니다.

```javascript
var num = 10;
console.log(num.toString()); // "10"
console.log(num.toString(2)); // "1010"
```

##### toFixed()
- 지정한 만큼의 정확도로 소수점을 찍은 문자열을 반환합니다.

```javascript
console.log(num.toFixed(2)); // "10.00"
```

- 메서드를 호출한 객체의 소수점 뒤 자리 수가 매개변수로 지정한 자리 수보다 
크다면 다음과 같이 반올림합니다.
- 인터넷 익스플로러 9이상부터 정상적으로 작동합니다.
- 일반적으로 소수점 이하 20자리까지를 지원합니다. 일부 브라우저는 이 범위 
이상을 지원합니다.

```javascript
var num = 10.005;
console.log(num.toFixed(2)); // 10.01
```

##### toExponential()
- 숫자를 지수 표기법 문자열로 반환합니다.

```javascript
var num = 10;
console.log(num.toExponential(1)); // 1.0e+1
```

##### toPrecision()
- 숫자에 따라 지수 표기법이나 소수점 표기법을 선택하여 반환합니다.
- 자신을 호출한 숫자형에 값에 따라 toFixed()나 toExponential() 중 하나를 호출합니다.
- 세 메서드는 모두 지정한 자리 수에 맞게끔 적절히 반올림하거나 내림합니다.
- 일반적으로 1부터 21 사이의 자리 수를 넘길 수 있습니다.

```javascript
var num = 99;
console.log(num.toPrecision(1)); // 1e+2
console.log(num.toPrecision(2)); // 99
console.log(num.toPrecision(3)); // 99.0
```

##### Boolean 객체와 비슷한 문제가 잠재하므로 사용을 피하는 편이 좋습니다.

```javascript
var numberObject = new Number(10);
var numberValue = 10;

console.log(typeof numberObject); // object
console.log(typeof numberValue); // number

console.log(numberObject instanceof Number); // true
console.log(numberValue instanceof Number); // false
```

#### 5.6.3 String 타입

- String 타입은 문자열을 나타내는 객체입니다.
- valueOf(), toLocaleString(), toString() 메서드는 모두 객체의 원시 문자열
값을 반환합니다.

```javascript
var stringObject = new String('Hello world');
```

##### length
주의할 점은 해당 문자열이 2바이트 문자이더라도 한 글자로 계산합니다.

```javascript
var stringValue = "Hello world";
console.log(stringValue.length); // 11
```

##### 글자 메서드

###### charAt()
매개변수로 받은 인덱스에 위치한 문자를 한 글자로 이루어진 문자열로 반환합니다.

```javascript
console.log(stringValue.charAt(1)); // e
```

###### charCodeAt()
매개변수로 받은 인덱스에 위치한 문자를 문자 코드로 반환합니다.

```javascript
console.log(stringValue.charCodeAt(1)); // 101
```

###### ECMAScript 5에서 개별 문자 접근 방법 - 대괄호 표기법

```javascript
console.log(stringValue[1]); // e
```

##### 문자열 조작 메서드
문자열 값을 조작하는 메서드는 다양합니다.

###### concat()
- 문자열을 병합하여 그 결과를 반환합니다.

```javascript
var stringValue = 'hello ';
var result = stringValue.concat('world');
console.log(result); // hello world
console.log(stringValue); // hello
```

- concat() 메서드가 받는 매개변수 숫자에는 제한이 없으므로 다음과 같이 문자열을 
원하는 만큼 넘길 수 있습니다.

```javascript
var stringValue = 'hello ';
var result = stringValue.concat('world', ' !!');
console.log(result); // hello world !!
```

- 연산자 `+` 가 더 자주 쓰이며 concat() 메서드보다 더 빨리 동작합니다.

###### slice(), substr(), substring()
- 세 메서드는 모두 자신을 호출한 문자열의 일부분을 반환하며 매개변수는 한 개 
또는 두 개를 받습니다
- **두 번째 매개변수 사용이 다릅니다.**

```javascript
var stringValue = 'wonderful-life';

console.log(stringValue.slice(3)); // derful-life
console.log(stringValue.substring(3)); // derful-life
console.log(stringValue.substr(3)); // derful-life

console.log(stringValue.slice(3, 7)); // derf
console.log(stringValue.substring(3, 7)); // derf
console.log(stringValue.substr(3, 7)); // derful-
```

**음수를 넘겼을 경우**

- slice(): 음수 매개변수를 받으면 문자열 길이에 해당 매개변수를 더한 값을 사용합니다.
- substr(): 첫 번째 매개변수에 음수를 받으면 문자열 길이에 해당 매개변수를 
더한 값을 사용합니다. 두 번째 매개변수에 음수를 받으면 0을 사용합니다.
- substring(): 음수 매개변수를 모두 0으로 바꿉니다.

```javascript
var stringValue = 'wonderful-life';

console.log(stringValue.slice(-3)); // slice(11) = ife
console.log(stringValue.substr(-3)); // substr(11) = ife
console.log(stringValue.substring(-3)); // substring(0) = wonderful-life

console.log(stringValue.slice(3, -4)); // slice(3, 10) = derful-
console.log(stringValue.substring(3, -4)); // substring(3, 0) -> substring(0, 3) = won
console.log(stringValue.substr(3, -4)); // 빈 문자열
```

##### 문자열 위치 메서드 indexOf(), lastIndexOf()

- 문자열 안에서 원하는 문자열의 위치를 찾는 메서드입니다.
- 두 메서드는 모두 매개변수로 넘긴 문자열을 검색해 그 위치를 반환하며
찾지 못했을 때는 **-1**을 반환합니다.
- 두 메서드의 차이는 `indexOf()`가 문자열 처음에서 검색을 시작하는 반면
`lastIndexOf()`는 문자열 마지막에서 검색을 시작한다는 점입니다.

```javascript
var stringValue = 'hello world';
stringValue.indexOf('o'); // 4
stringValue.lastIndexOf('o'); // 7
```

각 메서드에 두 번째 매개변수 6을 넘기면 결과는 이전 예제와 반대가 됩니다.

```javascript
stringValue.indexOf('o', 6); // 7: 인덱스 6(w)부터 검색을 시작한다.
stringValue.lastIndexOf('o', 6); // 4: 인덱스 6부터 시작해 hello의 'o' 찾는다.
```

###### 원하는 문자를 전부 찾을 수 있는 방법
검색을 시작할 위치를 증가시키면서 indexOf()를 계속 호출합니다.

```javascript
var stringValue = 'Lorem ipsum dolor sit amet, consectetur adipisicing elit';
var positions = new Array();
var pos = stringValue.indexOf('e');

while(pos > -1) {
    positions.push(pos);
    pos = stringValue.indexOf('e', pos + 1);
}

console.log(positions); // [3, 24, 32, 35, 52]
```

##### trim() 메서드

문자열을 복사한 후 앞뒤 공백을 모두 제거한 결과를 반환합니다.

```javascript
var stringValue = '  delete space  ';
var trimmedStringValue = stringValue.trim();

console.log(stringValue); // '  delete space  '
console.log(trimmedStringValue); 'delete space'
```

##### 대소문자 메서드
대개는 지역 메서드와 범용 메서드가 완전히 같지만 터키어 같은 일부 언어에서는
유니코드 대소문자 변환에 따른 특별한 규칙이 필요하며 이 때문에 지역 메서드가 필요합니다.

###### toLowerCase(), toUpperCase()
java.lang.String의 해당 메서드를 본따 만들어진 메서드입니다.

###### toLocaleLowerCase(), toLocaleUpperCase()
지역에 맞게 사용하도록 만든 지역 메서드입니다.

```javascript
var stringValue = 'hello world';
console.log(stringValue.toLocaleUpperCase()); // HELLO WORLD
console.log(stringValue.toUpperCase()); // HELLO WORLD
console.log(stringValue.toLocaleLowerCase()); // hello world
console.log(stringValue.toLowerCase()); // hello world
```

##### 문자열 패턴 매칭 메서드

###### match()

- RegExp 객체의 **exec() 메서드와 같은 결과**를 반환합니다.
- 매개변수로 정규 표현식 리터럴이나 RegExp 객체를 하나 받습니다.

```javascript
var text = 'cat, bat, sat, fat';
var pattern = /.at/;

// pattern.exec(text)와 같습니다.
var matches = text.match(pattern);
console.log(matches.index); // 0
console.log(matches[0]); // cat
console.log(pattern.lastIndex); // 0
```

**lastIndex**
패턴 매칭을 어느 위치에서 시작할지 나타내는 정수 값입니다. 
이 값은 항상 0에서 시작합니다.

**index**
패턴이 일치한 위치를 나타냅니다.

###### search()

- match()와 마찬가지로 정규 표현식 리터럴이나 RegExp 객체를 매개변수롤 받습니다.
- 패턴에 일치하는 첫 번째 문자열 인덱스를 반환하며 일치하는 것을 찾지 
못했을 때는 **-1**을 반환합니다.
- 항상 문자열 처음에서 검색을 시작합니다.

```javascript
var text = 'cat, bat, sat, fat';
var pos = text.search(/at/);
console.log(pos); // 1
```

###### replace()

- 문자열 일부를 바꾸는 메서드입니다.
- 매개변수를 두 개 받는데 첫번째 매개변수는 RegExp 객체 또는 문자열(단,
이 문자열은 정규 표현식으로 변환되지 않습니다.)이고 두 번째 매개변수는 
문자열 또는 문자열을 반환하는 함수입니다.
- 첫 번째 매개변수가 문자열이라면 해당 문자열과 일치하는 첫 번째 문자열만 바꿉니다.
- 일치하는 문자열 전체를 바꾸려면 다음과 같이 정규표현식에 g 플래그를 써서 
넘기는 방법 외에는 없습니다.

```javascript
var text = 'cat, bat, sat, fat';

var result = text.replace('at', 'ond');
console.log(result); // cond, bat, sat, fat

var result2 = text.replace(/at/g, 'ond');
console.log(result2); // cond, bond, sond, fond
```

정규 표현식에서 얻은 정보를 다양한 방법으로 응용하는 특수문자가 있습니다. (195쪽)

```javascript
var text = 'cat, bat, sat, fat';
result = text.replace(/(.at)/g, 'word ($1)');
console.log(result); // word (cat), word (bat), word (sat), word (fat)

result2 = text.replace(/(.at)/g, 'word ($\')');
console.log(result2); // word (, bat, sat, fat), word (, sat, fat), word (, fat), word ()
```

- replace() 두 번째 매개변수에는 함수도 쓸 수 있습니다. 일치하는 것이 하나뿐일 때
콜백함수는 자동으로 매개변수를 세 개 받습니다. 
- 일치하는 문자열, 해당 문자열의 위치, 마지막으로 전체 문자열입니다.
- 매개변수로 함수를 넘기면 다음과 같이 대체할 문자열을 더 세밀히 조절할 수 있습니다.

```javascript
function htmlEscape(text) {
    return text.replace(/[<>"&]/g, function(match, pos, originalText) {
        switch(match) {
            case '<':
                return '&lt;';
            case '>':
                return '&gt;';
            case '&':
                return '&amp;';
            case '\"':
                return '&quot;';
        }
    });
}

// &lt;p class="greeting"&gt;Hello world!&lt;/p&gt;
console.log(htmlEscape('<p class=\"greeting\">Hello world!</p>'));
```

###### split()
- 텍스트 구분자를 기준으로 분리해서 배열에 담아 변환합니다.
- 구분자에는 문자열을 쓸 수도 있고, RegExp 객체를 쓸 수도 있는데 문자열을 
정규 표현식으로 간주하지는 않습니다.
- 옵션인 두 번째 매개변수는 반환 받을 배열의 크기를 지정하는 숫자입니다.
- split() 메서드 내의 정규 표현식 지원은 브라우저에 따라 다르므로,
캡쳐 그룹을 사용할 때는 브라우저별로 정확히 테스트하십시오.
- [브라우저 간 비호환성 문제에 관한 자세한 설명 - 자바스크립트 split 버그가 마침내 수정되었습니다.](http://blog.stevenlevithan.com/archives/cross-browser-split)

```javascript
var colorText = 'red,blue,green,yellow';
var colors1 = colorText.split(','); // ["red", "blue", "green", "yellow"]
var colors2 = colorText.split(',', 2); // ["red", "blue"]
```

##### localeCompare() 메서드
문자열 두 개를 비교한 후 다음과 같이 세 가지 값 중 하나를 반환합니다.

- 메서드를 호출하는 텍스트가 매개변수로 넘긴 문자열보다 알파벳 순서상 뒤에
있다면 음수를 반환합니다.(거의 대부분 -1 반환)
- 메서드를 호출한 텍스트와 매개변수 문자열이 일치한다면 0을 반화합니다.
- 메서드를 호출하는 텍스트가 매개변수로 넘긴 문자열보다 알파벳 순서상 앞에
있다면 양수를 반환합니다.(거의 대부분 1을 반환)

```javascript
var stringValue = 'yellow';
console.log(stringValue.localeCompare('brick')); // 1
console.log(stringValue.localeCompare('yellow')); // 0
console.log(stringValue.localeCompare('zoo')); // -1
```

`localeCompare()`에서 독특한 점은 메서드가 정확히 어떻게 동작할지는 브라우저를
실행하는 지역에 따라 다르다는 겁니다. ECMAScript에서 미국의 표준 언어는 영어이며
localeCompare()는 대소문자를 구분하고 대문자가 소문자보다 앞에 온다고 간주합니다.
하지만 지역에 따라 결과는 다를 수 있습니다.

##### fromCharCode() 메서드
문자 코드를 받아 이를 문자열로 변환하는 겁니다. 간단히 생각해 `charCodeAt()`
메서드가 하는 일을 거꾸로 한다고 생각하면 됩니다.

```javascript
console.log(String.fromCharCode(104, 101, 108, 108, 111)); // hello
```

##### HTML 메서드
웹 브라우저 제조사들은 자바스크립트에서 동적으로 HTML 형식을 생성할 필요가
있음을 일찍 깨달았습니다. 그에 따라 명세를 확장해서 HTML 형식 생성에 필요한
몇 가지 메서드를 추가하였습니다. 하지만 이들 메서드를 쓰면 시맨틱 마크업을
해치므로 거의 사용하지 않습니다.

















