---
layout: post
title: "책요약 - JavaScript for Web Developers 2"
excerpt: "언의어 기초(문법, 변수, 데이터 타입) 내용 정리"
categories: [js]
comments: false
---

> 자바스크립트 프로그래밍: 프론트엔드 개발자를 위한   
> 니콜라스 자카스    
> 인사이트 
> 978-89-6626-076-8

## 3장 언어의 기초 ##

### 3.1 문법 ###
C 언어, 자바나 펄 등 C와 비슷한 언어에서 차용한 것

#### 3.1.1 대소문자 구분

#### 3.1.2 식별자
- 첫 번째 문자는 반드시 글자나 밑줄(_), 달러 기호($) 중 하나여야 합니다.
- 다른 문자에는 글자나 밑줄, 달러 기호, 숫자를 자유롭게 쓸 수 있습니다.

#### 3.1.3 주석

#### 3.1.4 스트릭트 모드
스트릭트 모드는 기존과는 다른 방식으로 자바스크립트를 파싱하고 실행하라고 지시하는 것 ECMAScript 3판의 문제를 해결했으며 안전하지 않은 동작에는 에러를 반환하도록 합니다. 

``` javascript
"use strict";
```

인터넷 익스플로러 10+, 파이어폭스 4+, 사파리 5.1+, 오페라 12+, 크롬에서 스트릭트 모드를 지원

#### 3.1.5 문장
- 문장을 세미콜론으로 끝내지 않으면 압축했을 때 문법 에러가 발생할 수 있습니다.
- 제어문에 코드 블록( {} )을 쓰면 의도를 더 명확하게 표현할 수 있고 나중에 수정할 때 에러가 생길 가능성도 적습니다.

### 3.2 키워드와 예약어

### 3.3 변수
- ECMAScript는 느슨한 변수 타입을 사용하여, 어떤 타입의 데이터라도 저장할 수 있다. 
- 변수를 초기화하지 않으면 특별한 값 undefinded가 할당된다.
- 스트릭트 모드에서는 변수를 선언하지 않고 값을 할당하려 하면 **ReferenceError** 에러를 반환합니다.

### 3.4 데이터 타입

#### 3.4.1 typeof 연산자
typeof 연산자는 때때로 혼란스러운, 하지만 엄밀히 말해 올바른 값을 반환하므로 주의해야 합니다. typeof **unll**은 "object"를 반환하는데 null은 빈 객체를 참조하는 특별한 값이므로 이는 올바른 것입니다. 

- 정의되지 않은 변수: "undefined"
- 함수를 제외한 객체 또는 null: "object"

#### 3.4.2 undefined 타입
`var`를 써서 변수를 정의했지만 초기화하지 않았다면 해당 변수에는 다음과 같이 undefined가 할당됩니다.

#### 3.4.3 Null 타입
객체를 사용해야 하지만 해당 객체를 이용할 수 없을 때에는 항상 그 자리에 null이 와야 합니다. 이렇게 하면 **null이 빈 객체를 가리키는 포인터라는 점을 늘 숙지**할 수 있고 undefined와 구별할 수 있게 됩니다.

``` javascript
console.log(null == undefined)    // true
console.log(null === undefined)   // false
```

#### 3.4.4 불리언 타입
**Boolean()** : 항상 불리언 값을 반환

| 데이터 타입 | true로 변환되는 값              | false로 변환되는 값 |
|-------------|---------------------------------|---------------------|
| 불리언      | true                            | false               |
| 문자열      | 비어 있지 않은 문자열 모두      | "" (빈 문자열)      |
| 숫자        | 0이 아닌 모든 숫자. 무한대 포함 | 0, NaN              |
| 객체        | 모든 객체                       | null                |
| Undefined   | 해당 없음                       | undefined           |

#### 3.4.5 숫자 타입

##### 부동소수점 숫자
0.1과 0.2를 더하면 0.3이 아니라 **0.30000000000000004**를 반환합니다. 이런 반올림 에러 때문에 부동소수점 숫자를 평가하기가 어렵습니다. 따라서 부동소수점 숫자를 평가할 때는 이런 버그를 인지하고 다른 방법을 써야 합니다.

##### 숫자 범위
ECMAScript에서 표현할 수 있는 최솟값과 최대값 사이에 있는 유한한 값을 확인하려면 **isFinite()** 함수를 쓰면 된다. 이 함수는 매개변수가 최솟값과 최댓값 사이에 있을 경우에만 true를 반환합니다.

##### NaN: Not a Number
**isNaN()** : 이 함수는 매개 변수를 하나 받으면 해당 값이 '숫자가 아닌 값'인지 검사합니다.

``` javascript
console.log(isNaN("ten"));   // true
console.log(isNaN(10));      // false
console.log(isNaN(false));  // false
console.log(isNaN(true));   // false
```

##### 숫자 변환
- Number() : 어떤 데이터 타입도 가능

``` javascript
Number(null)    // 0
Number("")       // 0
Number(undefined)   // NaN
Number("ten")    // NaN
```

- parseInt() : 정수 형태의 문자열을 바꿀 때

``` javascript
parseInt("12apple")   // 12
parseInt(0.10)   // 0
parseInt("")    // NaN
parseInt("10", 10) // 두 번째 매개변수에 10진수 명시
```

- parseFloat() : 잘못된 부동소수점 숫자를 만날 때까지 파싱

``` javascript
parseFloat("1.25.23")   // 1.25
```

#### 3.4.6 문자열 타입

##### 문자열의 성질

##### 문자열로 변환

``` javascript
var value1 = null;
var value2;

value1.toString()   // Uncaught TypeError
String(value1)      // null

value2.toString()  //Uncaught TypeError
String(value2)    // undefined
```

1. **toString()**
    - null과 undefined에는 이 메서드가 존재하지 않습니다.
    - 기본값은 10진법: toString(10)
2. **String()**
toString() 메서드를 호출할 값이 null이나 undefined일 가능성이 있다면 값의 타입에 관계없이 항상 문자열을 반환하는 형 변환 함수 **String()**을 써도 됩니다.

#### 3.4.7 객체 타입

``` javascript
var o = new Object();
```

- **constructor** - 해당 객체를 만드는 데 쓰인 함수. 이전 예제에서는 Object() 함수가 생성자입니다.
- **hasOwnProperty( propertyName )** - 해당 프로퍼티가 객체 인스턴스에 고유하며 프로토타입에서 상속하지 않았음을 확인합니다. 프로퍼티 이름은 반드시 문자열이여야 합니다. 예를 들어 `o.hasOwnProperty("name")` 같은 형식으로 호출합니다.
- **isPrototypeOf( object )** -  해당 객체가 다른 객체의 프로토타입인지 확인합니다.
- **propertyIsEnumerable( propertyName )** - 해당 프로퍼티를 for-in 문에서 나열할 수 있는지 확인합니다. 프로퍼티 이름은 반드시 문자열이여야 합니다.
- **toLocaleString()** - 객체를 지역에 맞게 표현한 문자열을 반환합니다.
- **toString()** - 객체를 문자열로 변환해 반환합니다.
- **valueOf()** - 객체를 나타내는 문자열이나 숫자, 불리언을 반환합니다. toString()과 같은 값을 반환할 때가 많습니다. 

**ECMAScript에서는 모든 객체가 Object에 기반해 만들어지므로 이들 프로퍼티와 메서드는 모든 객체에 존재합니다.**
