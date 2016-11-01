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

##### 문자열 위치 메서드

커밍순~


















