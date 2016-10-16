---
layout: post
title: "책요약 - JavaScript for Web Developers 8"
excerpt: "참조타입(Function) 내용 정리"
categories: [js]
comments: false
---

## 5장 참조 타입

### 5.5 Function 타입
함수는 ECMAScript에서 가장 흥미로운 부분인데 이는 함수가 사실 객체라는 점에 기인합니다.

#### 함수 선언 문법(세미콜론 없음!)

```javascript
function sum(num1, num2) {
    return num1 + num2;
}
```

#### 함수 표현식(세미콜론 있음!)

```javascript
var sum = function (num1, num2) {
              return num1 + num2;
          };
```

#### Function 생성자
사실 이런 문법은 권장하지 않는데, 이런 문법을 쓰면 코드를 두 번, 즉 일반적인 ECMAScript 표현식으로서 평가하고 생성자에게 전달할 문자열을 다시 평가해야 하므로 성능에 영향이 있기 때문입니다.

```javascript
var sum = new Function('num1', 'num2', 'return num1 + num2'); // 권장하지 않음
```

#### 함수 이름은 단순히 함수를 가르키는 포인터일 뿐이므로 객체를 가리키는 포인터와 마찬가지입니다. 
즉, 다음과 같이 함수 하나에 이름을 여러 개 붙일 수 있습니다.

```javascript
function sum(num1, num2) {
    return num1 + num2;
}
console.log(sum(10, 10));        // 20

var anotherSum = sum();
console.log(anotherSum(20, 20)); // 40

sum = null;
console.log(anotherSum(40, 40)); // 80
```

- 괄호를 쓰지 않고 함수 이름만 쓰면 함수를 실행하지 않고 함수를 가르키는 포인터에 접근하는 것입니다.
- `sum`에 `null`을 할당하면 함수와의 연결이 사라지지만 `anotherSum()`은 아무 문제 없이 함수를 호출합니다.

#### 5.5.1 오버로딩 없음

```javascript
var addSomeNumber = function (num) {
    return num + 100;
}
addSomeNumber = function (num) {
    return num + 200;
}
addSomeNumber(100); // 300
```

이 예제에서는 함수 두 개에 같은 이름을 지정하므로 마지막에 정의한 함수가 이전에 정의한 함수를 덮어씀을 쉽게 이해할 수 있습니다.

#### 5.5.2 함수 선언 VS 함수 표현식
**자바스크립 엔진이 실행 컨텍스트에 데이터를 불러올 때 중요한 차이가 하나 있습니다.**
코드를 평가할 때 제일 먼저 함수 선언을 찾은 다음 이들을 맨 위로 올립니다(hoist).

```javascript
console.log(num(10, 1)); // 예기치 못한 식별자(Unexpected identifier)
var sum = function (num1, num2) {
    return num1 + num2;
}
```

#### 5.5.3 값처럼 쓰는 함수
함수를 다른 함수에 매개변수로 넘기거나, 함수가 실행 결과로 다른 함수를 반환하는 일이 가능합니다.

```javascript
function callSomeFunction(someFunction, someArgument) {
    return someFunction(someArgument);
}

function getGreeting(name) {
    return "Hello, " + name;
}

var result = callSomeFunction(getGreeting, "jay-j");
console.log(result);
```

#### 5.5.4 함수의 내부 구조

##### arguments 객체의 주요 목적은
함수 매개변수를 표현하는 것이지만, arguments 객체의 소유자인 함수를 가리키는 포인터인 callee라는 프로퍼티도 있습니다.
다음 계승(factorial)함수를 보십시오.

```javascript
function factorial(num) {
    if (num<=1) {
        return 1;
    } else {
        return num * factorial(num-1)
    }
}
```

계승 함수는 보통 위 예제처럼 재귀 함수로 구현합니다. 재귀 패턴은 함수 이름이 정해진 뒤 바뀌지 않을 때는 아무 문제도 없습니다.
바꿔 말해 이 함수가 제대로 실행되려면 함수 이름 "factorial"이 절대 바뀌지 말아야 합니다. 
다음과 같이 `arguments.callee`를 쓰면 재귀 함수가 함수 이름에 의존하는 약점을 극복할 수 있습니다.

```javascript
function factorial(num) {
    if (num<=1) {
        return 1;
    } else {
        return num * arguments.callee(num-1)
    }
}

var trueFactorial = factorial;
factorial = function () {
    return 0;
}; 

console.log(trueFactorial(5)); // 120
console.log(factorial(5)); // 0
```

함수에 대한 참조가 어떻게 바뀌더라도 재귀 호출은 정확히 이루어집니다.

##### this
`this`는 함수가 실행 중인 컨텍스트 객체에 대한 참조입니다.

```javascript
window.color = 'red';
var o = { color: 'blue' };

function sayColor() {
    console.log(this.color);
}

sayColor(); // red: this가 window를 가르킨다.

o.sayColor = sayColor;
o.sayColor(); // blue: this 객체는 o를 가르킨다.
```

##### caller
caller 프로퍼티에는 **해당 함수를 호출한 함수에 대한 참조**를 저장하며 전역 스코프에서 호출했다면 null이 저장됩니다.

```javascript
function outer() {
    inner();
}

function inner() {
    console.log(inner.caller);
}

outer(); 
```

함수와 이름 사이의 의존성을 제거하려면 `arguments.callee.caller`를 쓸 수 있습니다.

```javascript
function inner() {
    console.log(arguments.callee.caller);
}
```

###### 브라우저 지원
IE, FF, Chrome, Safari 모든 버전, Opera 9.6부터

###### 스트릭트 모드에서
arguments.caller와 함수의 caller 프로퍼티를 명확히 구분하기 위해 에러가 발생되고,
이렇게 구분한 데는 보안 목적도 있습니다. 써드파티 코드는 같은 컨텍스트에서 실행 중인 코드에 대해 알 수 없게 됩니다.

#### 5.5.5 함수 프로퍼티와 메서드

##### length 프로퍼티는 
함수가 넘겨받을 것으로 예상하는 이름 붙은 매개변수의 숫자입니다.

```javascript
function sayName(name) {
    alert(name);
}
console.log(sayName.length); // 1
```

##### prototype은
모든 참조 타입의 인스턴스 메서드가 존재하는 곳입니다.
- 즉 `toString()`이나 `valueOf()` 같은 메서드는 prototype에 존재하며 객체 인스턴스는 이에 접근합니다.
- prototype 프로퍼티는 개발자 자신만의 참조 타입과 상속을 정의할 때 매우 중요합니다.
- prototype 프로퍼티는 열거할 수 없는 프로퍼티이므로 `for-in`문에 나타나지 않습니다.

##### apply()
- apply() 메서드는 매개변수로 소유자 함수에 넘길 this와 매개변수 배열을 받습니다.
- 두 번째 매개변수는 **Array의 인스턴스일 수도 있고 arguments 객체**일 수도 있습니다.

```javascript
function sum(num1, num2) {
  return num1 + num2;
}

function callSum1(num1, num2) {
  return sum.apply(this, arguments); // arguments 객체를 넘깁니다.
}

function callSum2(num1, num2) {
  return sum.apply(this, [num1, num2]); // 배열을 넘깁니다.
}

console.log(callSum1(10, 10)); // 20
console.log(callSum2(10, 10)); // 20
```

##### call()
- apply()와 마찬가지로 동작하지만 매개변수를 전달하는 방식이 다릅니다.
- call()을 사용할 때는 반드시 다음 예제와 같이 매개변수를 각각 나열해야 합니다.

```javascript
function sum(num1, num2) {
    return num1 + num2;
}

function callSum(num1, num2) {
    return sum.call(this, num1, num2);
}

console.log(callSum(10, 10)); // 20
```

##### apply()와 call()의 진가는 매개변수를 전달해 호출하는 것이 아니라 this를 바꾸는 데 있습니다.  
call()이나 apply()를 써서 스코프를 바꾸면 객체마다 일일히 메서드를 등록하지 않아도 된다는 장점이 있습니다.

```javascript
window.color = "red";

var o = { color: 'blue' };

function sayColor() {
    console.log(this.color);
};

sayColor.call(this); // red
sayColor.call(window); // red
sayColor.call(o); // blue
```

##### bind()
이 메서드는 새 함수 인스턴스를 만드는데 그 this는 bind()에 전달된 값입니다.

```javascript
window.color = 'yellow';

var o = { color: 'green' };

function sayColor() {
    console.log(this.color);
}

var objectSayColor = sayColor.bind(o);
objectSayColor(); // green
```

###### bind() 브라우저 지원
IE 9 이상, FF 4 이상, Chrome, Safari 5.1 이상

##### toLocaleString(), toString()
- 함수에서 호출하면 항상 함수의 코드를 반환합니다.
- 디버그에는 유용할 수 있으나 중요한 기능에 그대로 사용해서는 안됩니다.

```javascript
sayColor.toString();

// result
"function sayColor() {
    console.log(this.color);
}"
```

##### valueOf()
함수 자체를 그대로 반환합니다.












