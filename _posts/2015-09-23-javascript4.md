---
layout: post
title: "JavaScript for Web Developers(4): 문장, 함수"
excerpt: "책요약: if, do-while, while, for, for-in, switch, 매개변수, arguments 객체"
categories: [js]
comments: false
---

> 자바스크립트 프로그래밍: 프론트엔드 개발자를 위한   
> 니콜라스 자카스    
> 인사이트
> 978-89-6626-076-8

### 3.6 문장

#### 3.6.1 if 문

```javascript
if (condition) statement1 else statement2
```

condition는 어떤 표현식이든 쓸 수 있다. `Boolean()` 함수를 호출해 불리언 값으로 바꾼다.

#### 3.6.2 do-while 문
do-while 문은 **평가 전 루프** 입니다. 평가전 루프라는 말은 루프의 종료 조건을 평가하기 전에 루프 본문을 실행한다는 뜻입니다. 즉 루프 본문은 최소 한 번은 반드시 실행됩니다.

```javascript
do {
    statement
} while (expression);
```

#### 3.6.3 while 문
while 문은 **평가 후 루프** 입니다. 평가 후 루프라는 말은 루프 본문을 실행하기 전에 종료 조건을 평가한다는 뜻입니다. 따라서 루프 본문을 단 한 번도 실행하지 않을 수도 있습니다.

```javascript
while(expression) statement
```

#### 3.6.4 for 문
for 문 역시 평가 후 루프입니다.

```javascript
for (initialization; expression; post-loop-expression) statement
```

변수 i가 루프 안에서 정의되었음에도 불구하고 루프 밖에서 이 변수에 접근할 수 있습니다.

```javascript
var count = 10;
for (var i=0; i<count; i++) {
    alert(i);
}
console.log(i);
```

#### 3.6.5 for-in 문
엄격한 반복문입니다. 객체의 프로퍼티를 나열하는 데 사용합니다.

```javascript
for (property in expression) statement
```

for 문과 마찬가지로 for-in 문 역시 제어부에서 반드시 var 키워드를 써야 하는 건 아니지만 **지역 변수를 이용하게끔 var 키워드를 쓰는 편** 이 좋습니다.

```javascript
for (var propName in window) {
    console.log(propName);
}
```

for-in 문은 프로퍼티를 나열할 객체를 가리키는 변수가 null이나 undefined라면 에러를 냅니다. ECMAScript 5에서는 이를 수정하여 에러를 내지 않고 단순히 루프 본문을 실행하지 않게 했습니다. **브라우저 호환성을 위해 for-in 루프를 실행하기 전에 객체를 가리키는 변수의 값이 null이나 undefined는 아닌지 확인하는 편이 좋습니다.**

#### 3.6.6 문장 레이블

```javascript
label: statement
```

```javascript
start: for (var i=0; i<count; i++) {
    alert(i);
}
```

start를 나중에  break나 coutinue 문에서 참조할 수 있습니다. 문장 레이블은 일반적으로 중첩된 루프에서 사용합니다.

문장 레이블과 break 및 continue 문을 조합하면 루프를 유연하게 만들 수 있지만 과용하면 디버그에 문제가 생길 수 있습니다. 레이블 이름은 항상 해당 레이블의 의도를 설명할 수 있게 정하고 루프를 너무 많이 중첩하지 않도록 하십시오.

#### 3.6.7 break 문과 coutinue 문
break 문은 즉시 루프에서 빠져나가 루프 다음 문장을 실행합니다.  

```javascript
var num = 0;
for (var i = 1; i < 10; i++) {
    if (i % 5 == 0) {
        break;
    }
    num++;
};

alert(num); // 4
```

continue 문은 루프를 즉시 빠져나가긴 하지만 루프 실행은 계속됩니다.

```javascript
var num = 0;
    for (var i = 1; i < 10; i++) {
        if (i % 5 == 0) {
            continue;
        }
        num++;
    };

alert(num); // 8
```

continue 문을 잘 사용하면 코드를 간결하게 작성할 수 있긴 하지만 자바스크립트 엔진에서 별도의 실행 컨텍스트를 만들고 관리해야 하므로 성능 문제가 생길 수 있습니다.

> "리팩터리을 통해 contiune 문을 제거했을 때 성능이 향상되지 않는 경우를 본 적이 없다."

continue 문은 개발자의 의도를 파악하기 어렵게 만들어 디버그나 유지 보수에도 문제가 생길 수 있습니다.

#### 3.6.8 with 문

```javascript
with (expression) statement;
```

with 문의 원래 의도는 다음과 같이 특정 객체를 코드에서 매우 자주 참조할 때 편라하게 작성하자는 것이었습니다.

```javascript
var qs = location.search.substring(1);
var hostName = location.hostname;
var url = location.href;

with (location) {
    var qs = search.substring(1);
    var hostName = hostname;
    var url = href;
}
```

**스트릭트 모드에서는 with 문을 금지하며 문법 에러로 간주합니다.**

#### 3.6.9 switch 문

```javascript
switch (expression) {
    case value: statement
        break;

    case value: statement
        break;

    default: statement;
}
```

- switch 문의 각 case는 '표현식이 value와 일치하면 statement를 실행하라'는 의미입니다.
- break 키워드를 쓰지 않으면 다음 case를 계속 평가합니다.
- default 키워드는 case 중 value로 평가되는 것이 없을 때 실행할 문장을 가리킵니다.
- 모든 데이터 타입에서 동작하므로 문자열과 객체에서도 사용할 수 있습니다.
- 값은 상수일 필요가 없으며 변수나 표현식도 쓸 수 있습니다.
- swith 문은 일치 연산자(`===`)로 값을 비교하므로 타입 변환은 일어나지 않습니다.

**case 문이 다음 case 문까지 진행하게 해야 한다면, 다음과 같이 주석을 달아서 break 문을 의도적으로 생략했으며 실수가 아님을 분명히 나타내십시오.**

```javascript
switch (i) {
    case 25:
        /* 계속 진행함 */

    case 35:
        alert("25 or 35");
        break;

    case 45:
        alert("45");
        break;

    default:
        alert("Other");
}
```

### 3.7 함수

함수는 문장을 캡슐화하여 어디서든, 언제든 실행할 수 있게 하므로 모든 언어의 핵심입니다.

```javascript
function functionName(arg0, arg1, ... , argN) {
    statement
}
```

일반적으로 함수에서 값을 반환할 필요가 없고 함수 실행을 멈추기만 하려 할 때 다음 예제처럼 사용하며 alert()은 표시되지 않습니다.

```javascript
function sayHi(name, message) {
    return;
    alert('Hello ' + name + ', ' + message); // 결코 호출되지 않습니다.
}
```

**함수는 항상 값을 반환하거나 항상 반환하지 않게 만들기를 권합니다. 반환에 일관성이 있어야 합니다.**

#### 3.7.1 매개변수의 이해

- 매개변수를 한 개, 세 개, 또는 아예 넘기지 않더라도 인터프리터는 이를 에러로 간주하지 않습니다.
- ECMAScript의 매겨변수가 내부적으로는 배열로 표현되기 때문입니다.
- 배열처럼 동작하기는 하지만 Array의 인스턴스는 아닙니다.
- 함수는 arguments라는 객체를 하나 갖는데, 이 객체를 통해 매개변수의 값에 접근할 수 있습니다.

다음과 같이 매겨변수에 명시적인 이름을 정하지 않고 쓸 수도 있습니다.

```javascript
function sayHi() {
    alert('Hello ' + argument[0] + ', ' + argument[1]);
}
```

arguments 객체의 length 프로퍼티를 통해 함수에 매개변수가 몇 개 전달되었는지 알 수있습니다. 이런 방법을 통해 개발자는 함수가 받는 매개변수 숫자에 제한을 두지 않고 넘겨받은 매개변수 개수에 맞게 반응할 수 있습니다.

```javascript
function doAdd() {
    if (arguments.length == 1) {
        console.log(argument[0] + 10);
    } else if (arguments.length == 2) {
        console.log(argument[0] + argument[1]);
    }
}
doAdd(10);
doAdd(30, 20);
```

매개변수에서 또 다른 중요한 점은 다음과 같이 arguments 객체를 이름 붙은 매개변수와 함께 쓸 수 있다는 겁니다.

```javascript
function doAdd(num1, num2) {
    if (arguments.length  == 1) {
        alert(num1 + 10);
    } else if (arguments.length == 2) {
        alert(arguments[0] + num2);
    }
}

doAdd(10);
doAdd(100, 200);
```

arguments 객체에서 한 가지 더 재미있는 점은 이 객체의 프로퍼티 값을 이에 대응하는 이름 붙은 매개변수에서 자동으로 반영한다는 점입니다.

```javascript
function doAdd(num1, num2) {
    arguments[1] = 10;
    alert(arguments[0] + num2);
}

doAdd(5, 100); // 15
```

num2, argument[1] 둘은 각각 다른 메모리 공간을 사용하지만 값은 반영됩니다. 그런데 이는 동기화가 아니라 단방향 반영입니다. 즉 이름 붙은 매개변수의 값을 바꾸더라도 arguments의 해당 프로퍼티는 **바뀌지 않습니다.**

함수를 정의할 때 함께 정의한 매개변수를 넘기지 않으면 해당 매개변수에는 자동으로 undefined가 할당됩니다. 이는 변수를 정의하기만 하고 초기화하지는 않는 것과 비슷합니다. 예를 들어 doAdd() 함수를 호출할 때 매개변수를 하나만 넘기면 num2에는 undefined가 할당됩니다.

#### 3.7.2 오버로딩 없음

```javascript
function addSomeNumber(num) {
    return num + 100;
}

function addSomeNumber(num) {
    return num + 200;
}

var result = addSomeNumber(100); // 300
```

함수에 넘긴 매개변수의 타입과 숫자를 체크해서 그에 맞게 반응하는 방법으로 오버로딩을 흉내낼 수 있습니다.

### 3.8 요약
- 스트릭트 모드는 자바스크립트에서 에러가 자주 생기는 부분에 몇 가지 제약을 가한 겁니다.
- ECMAScript의 함수는 다른 언어의 함수와 다르게 동작합니다.
- 값을 반환하지 않는 함수는 사실 특별한 값 undefined를 반환합니다.
